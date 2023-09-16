# COP5615 - Distributed Operating Systems Principles - Bitcoin-minning

### Team Members
- **Namita Namita** (UFID: 48479313)
- **Shriyans Nidhish** (UFID: 19616510)

### Problem Statement 
The goal of this project is to utilize Erlang and the actor model to implement a bitcoin mining simulator. The simulator identifies the string appended with the UFID so that the hash for the string, using the SHA256 hashing algorithm, has `k` or more preceding zeroes. We aim to craft a robust multi-core-compatible solution using Erlang and the Actor Model.

### Example 
When the input is `6`, the output "namitanamita;lkfs70 `0000007EB01A9C5C75868832211F9E5B148A4076D9197323F594B8098C8E701B`" indicates that the coin with 6 leading 0's is "namitanamita;lkfs70" prefixed by the Gatorlink ID "namitanamita".

### Implementation 
Our approach to bitcoin mining using Erlang's actor model involves delegating actors (processes) based on input size. These actors perform hashing on the inputs, verifying if the hashed string has the specified number of leading zeroes. Once computation is complete, the result, i.e., the mined bitcoin, is sent out.

- **Input (leading number of zeros)**: 4
- **Number of workers delegated**: 8
- **Total process**: 9 (8 workers, 1 boss)
- **Bitcoins per actor**: 4
- **Total Bitcoins mined**: 33 (including 1 coin from boss)

### Execution 
1. **Step 1**: Created new node for each actor on 2 different machines (1 boss node, 4 actor nodes on the first machine and 4 actor nodes on the second machine).
    ```shell
    erl -name boss@192.168.0.46 -setcookie dosp
    ```
2. **Step 2**: Connect every node with each other and the boss (both machines).
    ```erlang
    net_adm:ping(‘worker1@192.168.0.46’)
    ```
3. **Step 3**: Compile the program on each node, including the boss.
    ```erlang
    c(bitcoinminenew)
    ```
4. **Step 4**: Run the program from the boss node.
    ```erlang
    bitcoinminenew:main()
    ```

### Output
**Case 1**: Input leading zeros = 4

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/019ef4f6-a928-4bb0-aefb-7d63f5ab2837)

Fig 1: Coins mined with 4 leading zeros.

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/655cf125-5c7f-4e12-a5ba-acd94bcbc7f8)

Fig 2: CPU core usage before mining 1

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/8ad5dde8-ff2f-469e-bbfa-88c4a5a33d4a)

Fig 3: - CPU core usage while mining 1

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/7eb5b829-d47e-41e0-8233-cefca345599d)

Fig 4: - Core usage before and while mining of machine 2.


**Case 2**: Input leading zeros = 6

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/1759ff09-6151-474a-91c3-707feef159b1)

Fig 5: Coins mined with 6 leading zeros.

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/147de2b9-4433-4d99-80c2-af87a6381c33)

Fig 6: - Boss connected to all the nodes on machine 1 and machine 2

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/dd5ca55e-c78c-4007-89c4-81bb86ffafe3)

Fig 7: - Activity monitor of machine 1 with 1 boss and 4 workers node before mining.

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/42bfedaa-4aa0-4e2f-bc25-543df44aa4dc)

Fig 8: - CPU usage of machine 1 before mining.

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/e10da9b8-77af-4ef0-91b9-c7000fe0eb49)

Fig 9: - Activity monitor and CPU usage of machine 1 with 1 boss and 4 workers node while mining.

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/ff84977b-4a58-48ee-ad90-0dee6fc83501)

Fig 10: - Activity monitor and CPU usage of machine 1 with 1 boss and 4 workers node after mining.

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/3ff30ff0-8c4d-4d94-8f56-c3bf2a88ab3a)

Fig 11: - Activity monitor of machine 2 with 4 workers node before mining.

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/45b0f3aa-6514-4c44-b2f1-4c66393448a4)

Fig 12: - CPU usage of machine 2 before mining.

![image](https://github.com/shriyansnidhish/Bitcoin-minning/assets/38129645/0e3f75a0-7b7a-4894-b909-71d9277e4f5d)

Fig 13: - Activity monitor and CPU usage of machine 2 with 4 workers node while mining.



### Output analysis
| No of leading zeros (K) | No of workers used | No of Strings per worker | Size of work unit (total strings/no of workers) | Running time | Coin with most 0s | Largest no of machines used |
|-------------------------|--------------------|--------------------------|-------------------------------------------------|--------------|--------------------|-----------------------------|
| 4                       | 8                  | 4                        | 32/8 = 4                                         | CPU time = 5.2, Real time = 1.13, Ratio = CPU/Real = 4.60 | 5   | 2                      | 
| 4                       | 2                  | 4                        | 32/4 = 8                                         | CPU time: 2.4, Real time = 0.68, CPU/Real = 3.52           | 5  | 2                       | 
| 6                       | 2                  | 6                        | 32/8 = 4                                         | CPU time: 13.8, Real time = 6.03, CPU/Real = 2.29          | 7  | 2                       | 




### Used machine Configurations
- **Machine 1** (MacBook Pro 14inch 2021)
  - RAM: 16GB
  - Processor: M1 Pro
  - SSD: 512GB
  - Cores: 8

- **Machine 2** (MacBook Air 2020)
  - RAM: 16GB
  - Processor: M1
  - SSD: 256GB
  - Cores: 8
