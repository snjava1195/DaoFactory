# DaoFactory

# Steps for setting up environment and deploying DaoFactory

1.$ tonos-cli config --url main.ton.dev 
	- set up a network

2. $ solc DaoFactory.sol
	- output: 
		- Code was generated and saved to file DaoFactory.code
		- ABI was generated and saved to file DaoFactory.abi.json
      
3. $ tvm_linker compile DaoFactory.code -o DaoFactory.tvc
	- output: 
		- ABI_PATH (obtained from INPUT): DaoFactory.abi.json
		- TVM_LINKER_LIB_PATH: "/home/visnja/TON-Solidity-Compiler/lib/stdlib_sol.tvm"
		- Contract successfully compiled. Saved to file DaoFactory.tvc.
		- Contract address: 9e3726423e9c93911c6a61e1de2b64839c59be39428f4815cf6fbb65eacaf2e9
          
4. $ tonos-cli genaddr --genkey key.json --wc 0 DaoFactory.tvc --abi DaoFactory.abi.json
	- With genaddr command you will get the  raw address of the contract - address of the contract after deploy 
  
5. $ tonos-cli deploy --sign key.json --wc 0 --abi DaoFactory.abi.json DaoFactory.tvc {}
	- output: Deploying...
		- MessageId: c5d56dc61b72926b2ade168fdd6f5b16e9bf48a2bc4033b636d55af51e3d6afe
		- Transaction succeeded.
		- Contract deployed at address:  0:738aaa39514f542b69239acfa2134d8f6f62d1191e6ac053a8a690610afe480d
		
    
# DaoRoot deploying steps
		
1. After you successfully deployed DaoFactory you will need to generate Platform.tvc file in order do decode it and use it for DAO deployment later:

	$ solc Platform.sol
  
	$ tvm_linker compile Platform.code -o Platform.tvc
  
	$ tvm_linker decode --tvc DaoFactory.tvc
		output: 
			Decoded:
			StateInit
			 split_depth: None
			 special: None
			 data: te6ccgEBAgEAKAABAcABAEPQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAg
			 code: te6ccgECEgEAAp4ABCSK7VMg4wMgwP/jAiDA/		 uMC8gsPAgERAr7tRNDXScMB+GYh2zzTAAGOHYECANcYIPkBAdMAAZTT/wMBkwL4QuIg+GX5EPKoldMAAfJ64tM/AfhDIbnytCD4I4ED6KiCCBt3QKC58rT4Y9MfAfgjvPK50x8B2zzyPAUDA0rtRNDXScMB+GYi0NcLA6k4ANwhxwDjAiHXDR/yvCHjAwHbPPI8Dg4DAzwgghANdPz5uuMCIIIQLvqJVLrjAiCCEGi1Xz+64wIJBgQCSDD4Qm7jAPhG8nPR+ELDAPhC+EUgbpIwcN66sPLj6fgA2zzyAAUKAT7tRNDXScIBjhRw7UTQ9AWAQPQO8r3XC//4YnD4Y+MNDQIqMPhG8uBMIZPU0dDe+kDR2zzjAPIABwoBToj4QsMA+EL4RSBukjBw3rqw8uvp+AD4AMjPhYjOgG/PQMmBAID7AAgANk9ubHkgdGhlIG93bmVyIGNhbiBvcGVyYXRlIQOsMPhG8uBM+EJu4wAhmNTTH9Mf1NHQldTTH9Mf4tN/0x/Tf9MfVVBvBgHR2zwhjh8j0NMB+kAwMcjPhyDOcc8LYQHIz5I10/Pmzs3JcPsAkTDiMNs88gANCwoAHPhD+ELIy//LP8+Dye1UAeb4APgoASJwyMv/cG2AQPRDyPQAyVUDyM+EgPQA9ADPgckg+QDIz4oAQMv/ydBVMCTIz4WIzoKAIdzWUAAAAAAAAAAAAAAAAAADzwuOIds8zM+DVSDIz5HTKxgyzAFvJl5Qyx/LH8t/yx/Lf8sfzs3JcPsADAA00NIAAZPSBDHe0gABk9IBMd70BPQE9ATRXwMAHu1E0NP/0z/TADHR+GP4YgAK+Eby4EwCCvSkIPShERAAFHNvbCAwLjU5LjAAAA==
			 code_hash: e7aad26b7b4417579f101524af6ae4c619eea1bdfc8dfc082fe72165a30736b7
			 data_hash: 55a703465a160dce20481375de2e5b830c841c2787303835eb5821d62d65ca9d
			 code_depth: 5
			 data_depth: 1
			 version: sol 0.59.0
			 lib:  None
			 
	- The code data from the output is platformCode_ parameter for deploying new DaoRoot
       
# In the next steps, ever.bytie.moe/executor is being used

2. DaoFactory contract address input

 ![image_2022_07_16T09_39_04_358Z](https://user-images.githubusercontent.com/32481282/179352007-51d607c4-a319-46da-945a-91ffb3fe45e7.png)
 
 
3. Load DaoFactory.abi.json file by clicking on 'From file' button

 ![image_2022_07_16T09_40_01_816Z](https://user-images.githubusercontent.com/32481282/179352107-4ee02706-7e1b-4444-a725-790ad0d1fa92.png)


4. DaoFactory contract overview

![image_2022_07_16T09_41_24_043Z](https://user-images.githubusercontent.com/32481282/179352160-7a374df9-0d75-4ee1-90d9-c8e265077db7.png)


5. By choosing 'deploy' function in the previous image, fill the neccessary parameters

![image_2022_07_16T09_42_19_201Z](https://user-images.githubusercontent.com/32481282/179352224-f6760c2b-82a8-4463-8cfc-1613b8cd041a.png)


6. After filling neccessary input fields, click one of the options to deploy DaoRoot

![image_2022_07_16T09_42_50_822Z](https://user-images.githubusercontent.com/32481282/179352283-5a62bf31-d31d-48e4-8016-64524a9372fd.png)


7. Output after choosing 'Send external' option

![image_2022_07_16T09_44_25_261Z](https://user-images.githubusercontent.com/32481282/179352324-967cc633-d69b-4389-a43c-adf6b8bbd08a.png)

