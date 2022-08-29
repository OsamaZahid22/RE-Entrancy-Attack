# Re-Entrancy

![image](https://user-images.githubusercontent.com/102557215/187306173-6cb3fb9f-fc74-478d-924c-c7ca2eeb03be.png)

 As the name suggest itself, Re-Entrancy means the hacker Re-Enter the function while still calling it. Re-Entrancy is one of the oldest security vulnerabilities that was discovered in smart contracts. It is the exact vulnerability that caused the infamous 'DAO Hack' of 2016. Over 3.6 million ETH was stolen in the hack, which today is worth billions of dollars.

Re-Entrancy is the vulnerability in which if Contract A calls a function in Contract B, Contract B can then call back into Contract A while Contract A is still processing.

This can lead to some serious vulnerabilities in Smart contracts, often creating the possibility of draining funds from a contract.

Let's understand how this works with the example shown in the above diagram. Let's say Contract A has some function - call it f() that does 3 things:

Checks the balance of ETH deposited into Contract A by Contract B
Sends the ETH back to Contract B
Updates the balance of Contract B to 0
Since the balance gets updated after the ETH has been sent, Contract B can do some tricky stuff here. If Contract B was to create a fallback() or receive() function in it's contract, which would execute when it received ETH, it could call f() in Contract A again.

Since Contract A hasn't yet updated the balance of Contract B to be 0 at that point, it would send ETH to Contract B again - and herein lies the exploit, and Contract B could keep doing this until Contract A was completely out of ETH.


![image](https://user-images.githubusercontent.com/102557215/187306603-b5f690a1-8f5b-4854-b0a7-be35d2638fd4.png)
