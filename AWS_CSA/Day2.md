# Day2 Topic Covered 
1. 👉 What is instances?
2. 👉What is sleep mode?
3. 👉 What is console?
4. 👉 What is difference b/w window edition os and server edition os?
5. 👉 What is ssh?
6. 👉 Format of key
 7. 👉 Which format of key putty support?
## Answer
1. Instances in AWS are basically virtual environments. These virtual environments are isolated from the underlying base OS. It’s an On-demand service, i.e. a user can rent the virtual server(instances) on an hourly base and deploy their applications on it.
2. Hibernation is also something like sleep mode with only difference that when u put it in hibernation mode, the data will be persistent and get stored in the hard disk so we won't ever lose our data process(In this, all the data of the RAM internally gets stored in the hard disk) https://aws.amazon.com/blogs/aws/new-hibernate-your-ec2-instances/
3. The console is the text output device for system administration messages. These messages come from the kernel, from the init system and from the system logger.
4. https://www.quadricsoftware.com/2016/01/29/4-key-differences-between-a-windows-server-and-a-windows-desktop-installation/
5. The SSH protocol (also referred to as Secure Shell) is a method for secure remote login from one computer to another, It is a secure alternative to the non-protected login protocols (such as telnet, rlogin) and insecure file transfer methods (such as FTP).
6. The keys that Amazon EC2 uses are 2048-bit SSH-2 RSA keys.
7. The default format of key is .pem and we need to convert .pem format into .ppk format because putty supports .ppk (putty private key) format. The key can be converted using puttygen software." PuTTY doesn't support the SSH private key format created by the Oracle Cloud wizards. You need to convert the private key to the PuTTY required format. To connect to a remote machine with PuTTY, your private key should have a ppk format."

