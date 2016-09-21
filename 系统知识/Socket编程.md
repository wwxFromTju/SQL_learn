### Java client (UDP)

```
import java.io.*; 
import java.net.*; 
  
class UDPClient { 
    public static void main(String args[]) throws Exception 
    { 
  
      BufferedReader inFromUser = new BufferedReader(new InputStreamReader(System.in)); 
  
      DatagramSocket clientSocket = new DatagramSocket(); 
  
      InetAddress IPAddress = InetAddress.getByName("hostname"); 
  
      byte[] sendData = new byte[1024]; 
      byte[] receiveData = new byte[1024]; 
  
      String sentence = inFromUser.readLine(); 
      sendData = sentence.getBytes();  
        
      DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, IPAddress, 9876); 
  
      clientSocket.send(sendPacket); 
  
      DatagramPacket receivePacket = 
         new DatagramPacket(receiveData, receiveData.length); 
  
      clientSocket.receive(receivePacket); 
  
      String modifiedSentence = 
          new String(receivePacket.getData()); 
  
      System.out.println("FROM SERVER:" + modifiedSentence); 
      clientSocket.close(); 
      } 
} 
```     

### Java Server (UDP)

```
import java.io.*; 
import java.net.*; 
  
class UDPServer { 
  public static void main(String args[]) throws Exception 
    { 
  
      DatagramSocket serverSocket = new DatagramSocket(9876); 
  
      byte[] receiveData = new byte[1024]; 
      byte[] sendData  = new byte[1024]; 
  
      while(true) 
        { 
  
          DatagramPacket receivePacket = 
             new DatagramPacket(receiveData, receiveData.length); 
           serverSocket.receive(receivePacket); 
           
          String sentence = new String(receivePacket.getData()); 
  
          InetAddress IPAddress = receivePacket.getAddress(); 
  
          int port = receivePacket.getPort(); 
  
          String capitalizedSentence = sentence.toUpperCase(); 

          sendData = capitalizedSentence.getBytes(); 
  
          DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, IPAddress, port); 
  
          serverSocket.send(sendPacket); 
        } 
    } 
}  
```

### Java client (TCP)

```
import java.io.*; 
import java.net.*; 
class TCPClient { 

    public static void main(String argv[]) throws Exception 
    { 
        String sentence; 
        String modifiedSentence; 

        BufferedReader inFromUser = 
          new BufferedReader(new InputStreamReader(System.in)); 

        Socket clientSocket = new Socket("hostname", 6789); 

        DataOutputStream outToServer = new DataOutputStream(clientSocket.getOutputStream()); 

        BufferedReader inFromServer = new BufferedReader(new InputStreamReader(clientSocket.getInputStream())); 

        sentence = inFromUser.readLine(); 

        outToServer.writeBytes(sentence + '\n'); 

        modifiedSentence = inFromServer.readLine(); 

        System.out.println("FROM SERVER: " + modifiedSentence); 

        clientSocket.close(); 
                   
    } 
} 
```

### Java server (TCP)

```
import java.io.*; 
import java.net.*; 

class TCPServer { 

  public static void main(String argv[]) throws Exception 
    { 
      String clientSentence; 
      String capitalizedSentence; 

      ServerSocket welcomeSocket = new ServerSocket(6789); 
  
      while(true) { 
  
            Socket connectionSocket = welcomeSocket.accept(); 

           BufferedReader inFromClient = 
              new BufferedReader(new
              InputStreamReader(connectionSocket.getInputStream())); 

           

           DataOutputStream  outToClient = 
             new DataOutputStream(connectionSocket.getOutputStream()); 

           clientSentence = inFromClient.readLine(); 

           capitalizedSentence = clientSentence.toUpperCase() + '\n'; 

           outToClient.writeBytes(capitalizedSentence); 
        } 
    } 
} 
 
```

