# P2P Downloads 

## User Story



##Workflow 
TBD

##Public APIs


## P2PManager

###Public methods
 d. provider: video’s provider 
4. void switchContext(P2PContext)

##Peer
A class which represents a peer and contains following information:
```

## P2PEventListener

Public methods

###Reason error codes

int  RESULT_WIRELESS_IFACE_NOT_AVAILABLE  = 1; int  RESULT_DISCOVERY_FAILURE  = 2;
 int  RESULT_CONTENT_ALREADY_DOWNLOADED  = 14; int  RESULT_USER_NOT_INTERESTED  = 15;

#### SenderEventListener
Public methods

#### ReceiverEventListener
Public methods

### P2PContext
Class encapsulating context current device is under and has following fields. 

```
private  MODE  mMode ; // SENDER or RECEIVER
 private  P2PEventListener.EventListener  mListener ; // Can be SenderEventListener or ReceiverEventListener
```

1. Create P2PManager instance which is the entry point for P2P transfers and also the P2PEventListener: Managing P2PManager instance till P2P transfer is complete is Apps responsibility.

```
P2PManager  p2PManager  =  new  P2PManager(getApplicationContext()); P2PEventListener  p2PEventListener  =  new  P2PEventListener() {
```

2. Create P2PContext based on whether current peer is a SENDER or a RECEIVER, and set up the P2PManager. Below example shows what SENDER peer would do:

```
```

createContext  API is a utility method to create P2PContext by simply passing the  P2PContext.MODE . Its body is shown below which shows how  P2PEventListener.SenderEventListener  is set up for SENDER peer to listen for sender side notifications and similarly  P2PEventListener.ReceiverEventListener is set up to listen for receiver side notifications.

```
P2PContext createContext(P2PContext.MODE mode) {  peerList .clear();
Log. d ( TAG ,  " Receive Transfer complete-> contentId: "  + contentId +  ", provider: " +provider); }
```

3. Sender calls send API of P2PManager to send a content specified by content id/provider pair to the receiver peer (represented by Peer class) which is obtained in onPeerFound callback.

``` 
public void  onPeerFound(Peer peer) {  // update peerlist
```

4. Receiver can override onReceive callback shown above to determine whether it wants to receive the given content from the given Peer or not:

```
@Override
```

5. Finally, we must also stop P2PManager service so that all resources used by P2P are released properly. This may be called from onDestroy activity lifecycle method as shown below:

```
@Override
 }
```
 
