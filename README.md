# secure torrent

## Term Definitions
- node: any client software also downloading
- trusted node: a node that the user trusts with incriminating information on them selves.
- untrusted node: nodes the user has no knowledge who's behind that IP
- middle-man node: a node who transfers information from Alice to Bob, but does not know the content
- peer: another node that has/wants the content of a torrent

## Peer Discovery
through an empty torrent file as a way for all clients to connect off a tracker.

## Trusted Node Discovery
a query is passed through the web of nodes, starting with a set of untrusted nodes, going on through each of their trusted peers, avoiding cycles. It's returned with the IP of the trusted peer encrypted with the querier's public key.

## Finding Peers for a Torrent
a query is passed throug hthe web of nodes, only being passed to trusted nodes, recursively. A response is returned, encrypted at each stage. So if Alice is the querier, and Dave is a peer, Alice -> Bob -> Chris -> Dave, then it's encrypted with Alice(Bob(Chris(Dave's IP))) when it's returned to Alice.

## Downloading from a Peer
in the Alice -> Bob -> Chris -> Dave example, where Alice wishes to download from Dave. Alice takes an untrusted node, Eve, and asks her to collapse the list. Eve is given Bob(Chris(Dave's IP))), and asks Bob to decrypt, then Chris, then Dave. Dave responds with his own IP. Note that Eve didn't know about the search for peers, and has no knowledge of the data she's being asked to transfer. She now has Alice's and Dave's IPs, and can facilitate an encrypted transfer, where Dave is encrypting with a public key negotiated through the chain of trusted peers.
