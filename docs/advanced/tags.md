---
title: Follow the status of your upload
id: tags
---

In Swarm, an instruction to upload data to the network goes through 3 consecutive stages before it is completed:

- Splitting
- Storing
- Sending

In the splitting state, the file is deconstructed in *chunks* (Swarms canonical data unit) and packaged in a [*Binary Merkle Tree*](https://en.wikipedia.org/wiki/Merkle_tree). After splitting, the chunks are stored in your local database, where they directly enter a queue, to be sent to the network.

Sending starts immediately when the first chunks are split and stored. After the chunk is sent, you node will get a receipt from the node that stores the chunk, marking the completion of the upload for that chunk. After a receipt is received for all chunks, the upload is complete.

## How to track the status of your upload
The status of your upload can be followed by using `tags`. A `tag` is a label, given to all chunks that belong to the same upload instruction. 

:::info
The tag label is only known to your node. It is **not** communicated to the network, only your node will known that a set of chunks belong together.
:::

### Get the tag identifier
To get the status of an upload, we can:

1. Generate the tag before the upload and pass this tag on upload
2. Let the Bee node generate a tag automatically

The disadvantage of the second option is that you won't be able to follow the status of your upload while it is splitting (the tag-uid is communicated only after splitting is complete). To follow the status of splitting, you must generate the tag yourself beforehand.

Create a tag by sending a POST request to the `tag` API endpoint:

```console
curl -s -XPOST http://localhost:8083/tags | jq .uid
> 1620191689
```

Pass the returned uid to your next upload in the swarm-tag-uid header:

```console
curl -F file=@bee.jpg -H "swarm-tag-uid: <tag-uid-here>" http://localhost:8080/files
```

If you don't want to track splitting, do not include this header, and the `swarm-tag-uid` will be communicated as part of the normal upload response header.

:::info
You can view the response headers, including the swarm-tag-uid with curl by passing the `--verbose` flag with your upload instruction
:::

### Ask for the Current Status

To get the status of your upload, send a GET request to the `tag/<swarm-tag-uid>` API endpoint.

```console
curl http://localhost:8080/tags/<swarm-tag-uid> | jq
```

The response contains all the information that you need to follow the status of your file as it is synced with the network.

```json
{
  "total": 36, //the total number of chunks, 0 if the upload is still splitting
  "split": 36, //the current number of chunks which have been split and packed in the Binary Merkle Tree
  "seen": 0, //starts incrementing if the chunk is already seen before and sent to the network
  "stored": 36, //the total number of chunks stored and queued for sending (if not seen before)
  "sent": 36, //the total number of chunks sent to the network
  "synced": 0, //the total number of receipts received
  "uid": 4074122506,
  "name": "unnamed_tag_1598627762",
  "address": "",
  "startedAt": "2020-08-28T16:16:02.071929+01:00" //when the tag was created (ISO 8601 format)
}
```