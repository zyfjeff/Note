
# A New Direct Virtualized I/O Framework for NVMe SSDs

When a user sends an I/O request, it goes through the I/O stack in the virtual machine including file system and block layer, and finally arrives at the frontend component. Then,it is transferred to the backend via vRing. The backend invokes system calls to send the request into the Host-level OS. Then, the request goes through the I/O stack in the host machine and finally arrives NVMe hardware queues

we collect I/O traces and observe that there is a delay between an I/O completion in an NVMe device and a notification of the I/O completion to a virtual machine. This is because the I/O completion monitored by a host NVMe driver is informed to the Virtio backend via a file system event notification mechanism asynchronously, which creates a problematic situation where the backend does not identify or notify the I/O completion to the virtual machine via vRing, even though the request has already finished. This observation leads us to design our adaptive polling mechanism.

![[Pasted image 20250212100444.png]]


![[Pasted image 20250212100415.png]]


Adaptive polling mechanism: A separated polling thread is woken up with the consideration of the expected completion time.

![[Pasted image 20250212103947.png]]