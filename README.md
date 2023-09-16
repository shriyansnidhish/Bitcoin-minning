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
- **Case 1**: Input leading zeros = 4
  - Fig 1: Coins mined with 4 leading zeros.
  - Fig 2: CPU core usage before mining 1
  - ... (similarly for other figures)

- **Case 2**: Input leading zeros = 6
  - Fig 5: Coins mined with 6 leading zeros.
  - ... (similarly for other figures)

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
