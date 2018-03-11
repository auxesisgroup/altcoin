# Step to create altcoin:

#### 1. `git clone https://github.com/litecoin-project/litecoin`
####  2. `git checkout  9cffb23`  //to get older version of repo
#### 3. Replace  all instances  “Litecoin” with “Altcoin” and  “litecoin” with “altcoin” in all files.
Replace  `const CScriptID& hash = boost::get<const CScriptID&>(address);` with `const CScriptID& hash = boost::get<CScriptID>(address);` in `src/rpcrawtransaction.cpp` file.
#### 4. Search  and replace all instances of “LTC” with “ALT” in all files.
#### 5. Change port and rpc port numbers for testnet and mainnet.
#### 6. Change the checkpoints in src/checkpoints.cpp file for mainnet and testnet:
checkpoints : An old block hash is hardcoded into litecoin software.
Checkpoints prevent various DoS attacks from nodes flooding unusable chains and attacks involving isolating nodes and giving them fake chains,
but it is primarily an optimization for the initial blockchain download.
comment all the checkpoints for now, later we can replace with altcoin checkpoints.



```
//*****************for mainnet **********************
static MapCheckpoints mapCheckpoints =
        boost::assign::map_list_of
//  (  1500, uint256("0x841a2965955dd288cfa707a755d05a54e45f8bd476835ec9af4402a2b59a2967"))
//  (  4032, uint256("0x9ce90e427198fc0ef05e5905ce3503725b80e26afd35a987965fd7e3d9cf0846"))
//  (  8064, uint256("0xeb984353fc5190f210651f150c40b8a4bab9eeeff0b729fcb3987da694430d70"))
//  ( 16128, uint256("0x602edf1859b7f9a6af809f1d9b0e6cb66fdc1d4d9dcd7a4bec03e12a1ccd153d"))
//  ( 23420, uint256("0xd80fdf9ca81afd0bd2b2a90ac3a9fe547da58f2530ec874e978fce0b5101b507"))
//  ( 50000, uint256("0x69dc37eb029b68f075a5012dcc0419c127672adb4f3a32882b2b3e71d07a20a6"))
//  ( 80000, uint256("0x4fcb7c02f676a300503f49c764a89955a8f920b46a8cbecb4867182ecdb2e90a"))
//   (120000, uint256("0xbd9d26924f05f6daa7f0155f32828ec89e8e29cee9e7121b026a7a3552ac6131"))
//  (161500, uint256("0xdbe89880474f4bb4f75c227c77ba1cdc024991123b28b8418dbbf7798471ff43"))
//  (179620, uint256("0x2ad9c65c990ac00426d18e446e0fd7be2ffa69e9a7dcb28358a50b2b78b9f709"))
//  (240000, uint256("0x7140d1c4b4c2157ca217ee7636f24c9c73db39c4590c4e6eab2e3ea1555088aa"))
//   (383640, uint256("0x2b6809f094a9215bafc65eb3f110a35127a34be94b7d0590a096c3f126c6f364"))
//   (409004, uint256("0x487518d663d9f1fa08611d9395ad74d982b667fbdc0e77e9cf39b4f1355908a3"))
//  (456000, uint256("0xbf34f71cc6366cd487930d06be22f897e34ca6a40501ac7d401be32456372004"))
//   (541794, uint256("0x1cbccbe6920e7c258bbce1f26211084efb19764aa3224bec3f4320d77d6a2fd2"))
//  (585010, uint256("0xea9ea06840de20a18a66acb07c9102ee6374ad2cbafc71794e576354fea5df2d"))
//  (638902, uint256("0x15238656e8ec63d28de29a8c75fcf3a5819afc953dcd9cc45cecc53baec74f38"))
       (  0, uint256("0x"))
        ;



static const CCheckpointData data = {
&mapCheckpoints,
//1410516073, // * UNIX timestamp of last checkpoint block
//4896865,    // * total number of transactions between genesis and last checkpoint
           //   (the tx=... number in the SetBestChain debug.log lines)

//7000.0     // * estimated number of transactions per day after checkpoint
};



//************for testnet************

static MapCheckpoints mapCheckpointsTestnet =
    boost::assign::map_list_of
//       (   546, uint256("0xa0fea99a6897f531600c8ae53367b126824fd6a847b2b2b73817a95b8e27e602"))
        (   0, uint256("0x"))
    ;
static const CCheckpointData dataTestnet = {
    &mapCheckpointsTestnet,
       //1365458829,
        //547,
       //576
};

```


#### 6. Change the DNS seeds node in src/net.cpp file for mainnet and testnet:

Upon startup, if peer node discovery is needed, the client then issues DNS requests to learn about the addresses of other peer nodes.
The client includes a list of host names for DNS services that are seeded.

comment all the DNS seeds nodes for now, later we can replace with altcoin DNS seeds nodes.


```
//*********** for mainnet*************
 static const char *strMainNetDNSSeed[][2] = {
    //  {"litecointools.com", "dnsseed.litecointools.com"},
    //  {"litecoinpool.org", "dnsseed.litecoinpool.org"},
    //  {"xurious.com", "dnsseed.ltc.xurious.com"},
    //  {"koin-project.com", "dnsseed.koin-project.com"},
    //  {"weminemnc.com", "dnsseed.weminemnc.com"},
     {NULL, NULL}
 };


//*********** for testnet*************


 static const char *strTestNetDNSSeed[][2] = {
    // {"litecointools.com", "testnet-seed.litecointools.com"},
    // {"xurious.com", "testnet-seed.ltc.xurious.com"},
    // {"wemine-testnet.com", "dnsseed.wemine-testnet.com"},
    {NULL, NULL}
};
```

#### 7. Change Hard Coded "Seed" Addresses in [src/net.cpp](https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/net.cpp#L1234).

The client contains hard coded IP addresses that represent litecoin nodes.

-comment all the Hard Coded "Seed" nodes for now, later we can replace with altcoin  seeds nodes.
```
unsigned int pnSeed[] =
{
    // 0x38a9b992, 0x73d4f3a2, 0x43eda52e, 0xa1c4a2b2, 0x73c41955, 0x6992f3a2, 0x729cb992, 0x8b53b205,
    // 0xb651ec36, 0x8b422e4e, 0x0fe421b2, 0x83c1a2b2, 0xbd432705, 0x2e11b018, 0x281544c1, 0x8b72f3a2,
    // 0xb934555f, 0x2ba02e4e, 0x6ab7c936, 0x8728555f, 0x03bfd143, 0x0a73df5b, 0xcd2b5a50, 0x746df3a2,
    // 0x7481bb25, 0x6f4d4550, 0x78582f4e, 0xa03a0f46, 0xe8b0e2bc, 0xa2d17042, 0x718a09b0, 0xdaffd4a2,
    // 0xbb1a175e, 0xb21f09b0, 0xb5549bc0, 0xe404c755, 0x95d882c3, 0xfff3692e, 0x3777d9c7, 0x425b2746,
    // 0x497990c6, 0xb2782dcc, 0xf9352225, 0xa75cd443, 0x4c05fb94, 0x44c91c2e, 0x47c6a5bc, 0xd606fb94,
    // 0xc1b9e2bc, 0x32acd23e, 0x89560da2, 0x5bebdad8, 0x3a210e08, 0xbdc5795b, 0xcc86bb25, 0xbe9f28bc,
    // 0xef3ff3a2, 0xca29df59, 0xe4fd175e, 0x1f3eaa6b, 0xacdbaa6b, 0xb05f042e, 0x81ed6cd8, 0x9a3c0cc3,
    // 0x4200175e, 0x5a017ebc, 0x42ef4c90, 0x8abfd143, 0x24fbf3a2, 0x140846a6, 0x4f7d9553, 0xeea5d151,
    // 0xe67c0905, 0x52d8048e, 0xcabd2e4e, 0xe276692e, 0x07dea445, 0xdde3f3a2, 0x6c47bb25, 0xae0efb94,
    // 0xf5e15a51, 0xaebdd25b, 0xf341175e, 0x46532705, 0xc47728bc, 0xe4e14c90, 0x9dc8f752, 0x050c042e,
    // 0x1c84bb25, 0x4f163b25, 0x1a017ebc, 0xa5282e4e, 0x8c667e60, 0xc7113b25, 0xf0b44832, 0xf1a134d0,
    // 0x973212d4, 0xd35cbb25, 0xd5123b25, 0x68220254, 0x7ad43e32, 0x9268e32e, 0xdf143b25, 0xaf04c436,
    // 0xaded0051, 0xfa86d454, 0x09db048e, 0x26003b25, 0x58764c90, 0x9a2f555f, 0x0c24ec97, 0x92123b25,
    // 0x0526d35f, 0x17db048e, 0xd2e42f4e, 0x38cca5bc, 0xc6320ab9, 0xe28ac836, 0xc560aa6b, 0xa5c16041,
    // 0x70a6f1c0, 0x011ec8c1, 0xd6e9c332, 0x131263c0, 0xa15a4450, 0xef218abc, 0x2729f948, 0x02835443,
    // 0x5614336c, 0xb12aacb2, 0xe368aa6b, 0x3cc6ffad, 0x36206494, 0x2c90e9c1, 0x32bb53d4, 0xca03de5c,
    // 0x775c1955, 0x19ef1ba3, 0x0b00dc1f, 0x244d0f40, 0x54d9e2bc, 0x25ced152, 0x967b03ad, 0x951c555f,
    // 0x4c3f3b25, 0x13f6f3a2, 0x17fca5bc, 0x0e2d306c, 0xacd8764b, 0xca230bcc, 0x8569d3c6, 0x3264d8a2,
    // 0xe8630905, 0x25e02a64, 0x3aba1fb0, 0x6bbdd25b, 0xee9a4c90, 0xcda25982, 0x8b3e804e, 0xf043fb94,
    // 0x4b05fb94, 0x0c44c052, 0xf403f45c, 0x4333aa6b, 0xc193484d, 0x3fbf5d4c, 0x0bd7f74d, 0x150e3fb2,
    // 0x8e2eddb0, 0x09daf150, 0x8a67c7c6, 0x22a9e52e, 0x05cff476, 0xc99b2f4e, 0x0f183b25, 0xd0358953,
    // 0x20f232c6, 0x0ce9e217, 0x09f55d18, 0x0555795b, 0x5ed2fa59, 0x2ec85917, 0x2bf61fb0, 0x024ef54d,
    // 0x3c53b859, 0x441cbb25, 0x50c8aa6b, 0x1b79175e, 0x3125795b, 0x27fc1fb0, 0xbcd53e32, 0xfc781718,
    // 0x7a8ec345, 0x1da6985d, 0x34bd1f32, 0xcb00edcf, 0xf9a5fdce, 0x21ccdbac, 0xb7730118, 0x6a43f6cc,
    // 0x6e65e262, 0x21ca1f3d, 0x10143b25, 0xc8dea132, 0xaf076693, 0x7e431bc6, 0xaa3df5c6, 0x44f0c536,
    // 0xeea80925, 0x262371d4, 0xc85c895b, 0xa6611bc6, 0x1844e47a, 0x49084c90, 0xf3d95157, 0x63a4a844,
    // 0x00477c70, 0x2934d35f, 0xe8d24465, 0x13df88b7, 0x8fcb7557, 0xa591bd5d, 0xc39453d4, 0xd5c49452,
    // 0xc8de1a56, 0x3cdd0608, 0x3c147a55, 0x49e6cf4a, 0xb38c8705, 0x0bef3479, 0x01540f48, 0xd9c3ec57,
    // 0xed6d4c90, 0xa529fb94, 0xe1c81955, 0xfde617c6, 0x72d18932, 0x9d61bb6a, 0x6d5cb258, 0x27c7d655,
    // 0xc5644c90, 0x31fae3bc, 0x3afaf25e, 0x98efe2bc, 0x91020905, 0xb566795b, 0xaf91bd5d, 0xb164d655,
    // 0x72eb47d4, 0xae62f3a2, 0xb4193b25, 0x0613fb94, 0xa6db048e, 0xf002464b, 0xc15ebb6a, 0x8a51f3a2,
    // 0x485e2ed5, 0x119675a3, 0x1f3f555f, 0x39dbc082, 0x09dea445, 0x74382446, 0x3e836c4e, 0x6e43f6cc,
    // 0x134dd9a2, 0x5876f945, 0x3516f725, 0x670c81d4, 0xaf7f170c, 0xb0e31155, 0xe271894e, 0x615e175e,
    // 0xb3446fd0, 0x13d58ac1, 0x07cff476, 0xe601e405, 0x8321277d, 0x0997548d, 0xdb55336c, 0xa1271d73,
    // 0x582463c0, 0xc2543025, 0xf6851c73, 0xe75d32ae, 0xf916b4dd, 0xf558fb94, 0x52111d73, 0x2bc8615d,
    // 0xd4dcaf42, 0x65e30979, 0x2e1b2360, 0x0da01d73, 0x3f1263c0, 0xd15c735d, 0x9cf2134c, 0x20d0048e,
    // 0x48cf0125, 0xf585bf5d, 0x12d7645e, 0xd5ace2bc, 0x0c6220b2, 0xbe13bb25, 0x88d0a52e, 0x559425b0,
    // 0x24079e3d, 0xfaa37557, 0xf219b96a, 0x07e61e4c, 0x3ea1d295, 0x24e0d852, 0xdde212df, 0x44c37758,
    // 0x55c243a4, 0xe77dd35f, 0x10c19a5f, 0x14d1048e, 0x1d50fbc6, 0x1570456c, 0x567c692e, 0x641d6d5b,
    // 0xab0c0cc6, 0xab6803c0, 0x136f21b2, 0x6a72545d, 0x21d031b2, 0xff8b5fad, 0xfd0096b2, 0x5f469ac3,
    // 0x3f6ffa62, 0x7501f863, 0x48471f60, 0xcccff3a2, 0x7f772e44, 0xc1de7757, 0x0c94c3cb, 0x620ac658,
    // 0x520f1d25, 0x37366c5f, 0x7594b159, 0x3804f23c, 0xb81ff054, 0x96dd32c6, 0x928228bc, 0xf4006e41,
    // 0x0241c244, 0x8dbdf243, 0x26d1b247, 0xd5381c73, 0xf3136e41, 0x4afa9bc0, 0xa3abf8ce, 0x464ce718,
    // 0xbd9d017b, 0xf4f26132, 0x141b32d4, 0x2ec50c18, 0x4df119d9, 0x93f81772, 0xd9607c70, 0x3522b648,
    // 0xf2006e41, 0x761fe550, 0x40104836, 0x55dffe96, 0xc45db158, 0xe75e4836, 0x8dfab7ad, 0xe3eff3a2,
    // 0x6a6eaa6b, 0x2177d9c7, 0x724ce953, 0xafe918b9, 0xf9368a55, 0xdc0a555f, 0xa4b2d35f, 0x4d87b0b8,
    // 0x93496a54, 0x5a5c967b, 0xd47028bc, 0x3c44e47a, 0x11c363c0, 0x28107c70, 0xb756a558, 0xb82bbb6a,
    // 0x285d49ad, 0x3b0ce85c, 0xe53eb45f, 0xa836e23c, 0x409f63c0, 0xc80fbd44, 0x3447f677, 0xe4ca983b,
    // 0x20673774, 0x96471ed9, 0x4c1d09b0, 0x91d5685d, 0x55beec4d, 0x1008be48, 0x660455d0, 0xf8170fda,
    // 0x3c21dd3a, 0x8239bb36, 0x9fe7e2bc, 0x900c47ae, 0x6a355643, 0x03dcb318, 0xefca123d, 0x6af8c4d9,
    // 0x5195e1a5, 0x32e89925, 0x0adc51c0, 0x45d7164c, 0x02495177, 0x8131175e, 0x681b5177, 0x41b6aa6b,
    // 0x55a9603a, 0x1a0c1c1f, 0xdb4da043, 0x3b9b1632, 0x37e08368, 0x8b54e260, 0xcd14d459, 0x82a663c0,
    // 0x05adc7dd, 0xe683f3a2, 0x4cddb150, 0x67a1a62e, 0x8c0acd25, 0x07f01f3e, 0x3111296c, 0x2d0fda2e,
    // 0xa4f163c0, 0xca6db982, 0x78ed2359, 0x7eaa21c1, 0x62e4f3a2, 0x50b81d73, 0xcd074a3a, 0xcb2d904b,
    // 0x9b3735ce, 0xab67f25c, 0xa0eb5036, 0x62ae5344, 0xe2569bb2, 0xc4422e4e, 0xab5ec8d5, 0xaa81e8dd,
    // 0xa39264c6, 0xf391563d, 0xb79bbb25, 0x174a7857, 0x0fd4aa43, 0x3e158c32, 0x3ae8b982, 0xea342225,
    // 0x48d1a842, 0xa52bf0da, 0x4bcb4a4c, 0xa6d3c15b, 0x49a0d35f, 0x97131b4c, 0xf197e252, 0xfe3ebd18,
    // 0x156dacb8, 0xf63328bc, 0x8e95b84c, 0x560455d0, 0xee918c4e, 0x1d3e435f, 0xe1292f50, 0x0f1ec018,
    // 0x7d70c60e, 0x6a29d5be, 0xf5fecb18, 0xd6da1f63, 0xccce1c2e, 0x7a289f5e, 0x2775ae47, 0x696df560,
    // 0x4dbe00ae, 0x474e6c5c, 0x604141d5, 0xaed0c718, 0x8acfd23e, 0x7ff4b84c, 0x4b44fc60, 0xdf58aa4f,
    // 0x9b7440c0, 0xb811c854, 0xd90ec24e, 0xcff75c46, 0xa5a9cc57, 0xb3d21e4c, 0x794779d9, 0xe5613d46,
    // 0x9478be43, 0xc5d11152, 0xe85fbb6a, 0x3e1ed052, 0xf747e418, 0x3b9c61c2, 0xb2532949, 0x43077432,
    // 0xa3db0b68, 0xb3b6e35a, 0x70361b6c, 0x3a8bad3e, 0x23079e3d, 0x09314c32, 0x92f90053, 0x4fc31955,
    // 0xa59b0905, 0x924128bc, 0x4e63c444, 0x344dc236, 0x43055fcb, 0xdc1a1c73, 0x38aaaa6b, 0xa61cf554,
    // 0x6d8f63c0, 0x24800a4c, 0x2406f953, 0x9558bb6a, 0x1d281660, 0x054c4954, 0x2de4d418, 0x5fdaf043,
    // 0xb681356c, 0xf8c3febc, 0x8854f950, 0x55b45d32, 0xde07bcd1, 0x156e4bda, 0x924cf718, 0xc34a0d47,
    // 0xdd5e1c45, 0x4a0d63c0, 0xaf4b88d5, 0x7852b958, 0x6f205fc0, 0x838af043, 0x45ac795b, 0x43bbaa6b,
    // 0x998d1c73, 0x11c1d558, 0x749ec444, 0x9a38c232, 0xad2f8c32, 0x3446c658, 0x8fe7a52e, 0x4e846b61,
    // 0x064b2d05, 0x0fd09740, 0x7a81a743, 0xf1f08e3f, 0x35ca1967, 0x24bdb17d, 0x144c2d05, 0x5505bb46,
    // 0x13fd1bb9, 0x25de2618, 0xc80a8b4b, 0xcec0fd6c, 0xdc30ad4c, 0x4009f3a2, 0x472f3fb2, 0x5e69c936,
    // 0x0380796d, 0xa463f8a2, 0xa46fbdc7, 0x3b0cc547, 0xb6644f46, 0x4b90fc47, 0x39e3f563, 0x72d81e56,
    // 0xe177d9c7, 0x95bff743, 0xea985542, 0xc210ec55, 0xeef70b67, 0xc9eb175e, 0x844d38ad, 0x65afa247,
    // 0x72da6d26, 0xed165dbc, 0xe8c83ad0, 0x9a8f37d8, 0x925adf50, 0x6b6ac162, 0x4b969e32, 0x735e1c45,
    // 0x4423ff60, 0xfa57ec6d, 0xcde2fb65, 0x11093257, 0x4748cd5b, 0x720c03dd, 0x8c7b0905, 0xba8b2e48
};
```


#### 8. Change the name of the litecoin-qt.pro file to altcoin-qt.pro in main folder.



#### 9. Change block time in [src/main.cpp](https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.cpp#L1099)

```
static const int64 nTargetSpacing = 1 * 10;     // 10 sec (by default its 2.5 * 60 in litcoin)
```


#### 10. Change re-targeting  in [src/main.cpp](https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.cpp#L1098)
 Difficulty is a measure of how difficult it is to find a new block.

```
static const int64 nTargetTimespan = 2.5 * 24 * 60 * 60; //2.5 days
```

 #### 11. Change first letter of an address in [src/base58.h](https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/base58.h#L275)

 ```
 PUBKEY_ADDRESS = 23;   //Altcoin addresses start with A.
 ```


#### 12.  Change halving in [src/main.cpp](https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.cpp#L1093).

- Change halving at every 840000 to 50 block in GetBlockValue() function at line : nSubsidy >>= (nHeight / 840000); .



```
int64 static GetBlockValue(int nHeight, int64 nFees)
{
    int64 nSubsidy = 50 * COIN;
    // Subsidy is cut in half every 840000 blocks, which will occur approximately every 4 years
  //  nSubsidy >>= (nHeight / 840000); // Litecoin: 840k blocks in ~4 years
    nSubsidy >>= (nHeight / 50);
    return nSubsidy + nFees;
}
```



#### 13.  Change mining reward in [src/main.cpp](https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.cpp#L1090) .



```

int64 static GetBlockValue(int nHeight, int64 nFees)
{
  //  int64 nSubsidy = 50 * COIN;
    int64 nSubsidy = 100 * COIN;
    // Subsidy is cut in half every 840000 blocks, which will occur approximately every 4 years
    nSubsidy >>= (nHeight / 840000); // Litecoin: 840k blocks in ~4 years
    return nSubsidy + nFees;
}
```



#### 14. Change coinbase maturity in [src/main.h](https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.h#L58).

 Coinbase (mining reward transaction) transaction outputs can only be spent after this number of new block.


```
    static const int COINBASE_MATURITY = 20;
```



#### 15. Modification in genesis block according to requirements in [src/main.cpp](https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.cpp#L2782) file(InitBlockIndex() function).
GBP:  Following parameter  changes  in  InitBlockIndex() function  will help to create custom genesis block:
-  const char* pszTimestamp : Any metadata that you want to store with your genesis block transaction.
- txNew.vout[0].nValue : Genesis block reward.( 50 * COIN by default)
- txNew.vout[0].scriptPubKey : scriptPubKey is your genesis block transaction address scriptPubKey.
- block.nTime : current timestamp.
- block.nNonce : Nonce that should satisfy POW.

## NOTE: this code will help you to generate POW for your custom genesis block

POWCODE:


```
if (true && block.GetHash() != hashGenesisBlock)
{
    printf("Searching for genesis block...\n");
    // This will figure out a valid hash and Nonce if you're
    // creating a different genesis block:
    uint256 hashTarget = CBigNum().SetCompact(block.nBits).getuint256();
    uint256 thash;
   char scratchpad[SCRYPT_SCRATCHPAD_SIZE];

   loop
    {
       scrypt_1024_1_1_256_sp(BEGIN(block.nVersion), BEGIN(thash), scratchpad);
       if (thash <= hashTarget)
           break;
        if ((block.nNonce & 0xFFF) == 0)
        {
            printf("nonce %08X: hash = %s (target = %s)\n", block.nNonce, thash.ToString().c_str(), hashTarget.ToString().c_str());
        }
        ++block.nNonce;
        if (block.nNonce == 0)
        {
            printf("NONCE WRAPPED, incrementing time\n");
           ++block.nTime;
        }
    }
    printf("block.nTime = %u \n", block.nTime);
    printf("block.nNonce = %u \n", block.nNonce);
    printf("block.GetHash = %s\n", block.GetHash().ToString().c_str());

    }

  ```


Steps to generate new genesis block.

1. Make changes in GBP Parameters according to requirements.

2. Comment line  assert(block.hashMerkleRoot == uint256("0x97ddfbbae6be97fd6cdf3e7ca13232a3afff2353e29badfab7f73011edd4ced9"));
(https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.cpp#L2809)

3. Paste POWCODE after the  assert(block.hashMerkleRoot == uint256("0x97ddfbbae6be97fd6cdf3e7ca13232a3afff2353e29badfab7f73011edd4ced9"));
 line .




Now the InitBlockIndex() function look like this(src/main.cpp).


```
    bool InitBlockIndex() {
        // Check whether we're already initialized
        if (pindexGenesisBlock != NULL)
            return true;

        // Use the provided setting for -txindex in the new database
        fTxIndex = GetBoolArg("-txindex", false);
        pblocktree->WriteFlag("txindex", fTxIndex);
        printf("Initializing databases...\n");

        // Only add the genesis block if not reindexing (in which case we reuse the one already on disk)
        ifvMerkleTree (!fReindex) {
            // Genesis Block:
            // CBlock(hash=12a765e31ffd4059bada, PoW=0000050c34a64b415b6b, ver=1, hashPrevBlock=00000000000000000000, hashMerkleRoot=97ddfbbae6, nTime=1317972665, nBits=1e0ffff0, nNonce=2084524493, vtx=1)
            //   CTransaction(hash=97ddfbbae6, ver=1, vin.size=1, vout.size=1, nLockTime=0)
            //     CTxIn(COutPoint(0000000000, -1), coinbase 04ffff001d0104404e592054696d65732030352f4f63742f32303131205374657665204a6f62732c204170706c65e280997320566973696f6e6172792c2044696573206174203536)
            //     CTxOut(nValue=50.00000000, scriptPubKey=040184710fa689ad5023690c80f3a4)
            //   vMerkleTree: 97ddfbbae6

            // Genesis block
            const char* pszTimestamp = "The Times 03/Jan/2009 Chancellor on brink of second bailout for banks";
            CTransaction txNew;
            txNew.vin.resize(1);
            txNew.vout.resize(1);
            txNew.vin[0].scriptSig = CScript() << 486604799 << CBigNum(4) << vector<unsigned char>((const unsigned char*)pszTimestamp, (const unsigned char*)pszTimestamp + strlen(pszTimestamp));
            txNew.vout[0].nValue = 100 * COIN;
            txNew.vout[0].scriptPubKey = CScript() << ParseHex("040184710fa689ad5023690c80f3a49c8f13f8d45b8c857fbcbc8bc4a8e4d3eb4b10f4d4604fa08dce601aaf0f470216fe1b51850b4acf21b179c45070ac7b03a9") << OP_CHECKSIG;
            CBlock block;
            block.vtx.push_back(txNew);
            block.hashPrevBlock = 0;
            block.hashMerkleRoot = block.BuildMerkleTree();
            block.nVersion = 1;
            block.nTime    = 1317972665;
            block.nBits    = 0x1e0ffff0;
            block.nNonce   = 2085981884;

            if (fTestNet)
            {
                block.nTime    = 1317798646;
                block.nNonce   = 385270584;
          vMerkleTree  }

            //// debug print
            uint256 hash = block.GetHash();
            printf("%s\n", hash.ToString().c_str());
            printf("%s\n", hashGenesisBlock.ToString().c_str());
            printf("%s\n", block.hashMerkleRoot.ToString().c_str());

            //   assert(block.hashMerkleRoot == uint256("0x97ddfbbae6be97fd6cdf3e7ca13232a3afff2353e29badfab7f73011edd4ced9"));

            if (true && block.GetHash() != hashGenesisBlock)
            {
                printf("Searching for genesis block...\n");
                // This will figure out a valid hash and Nonce if you're
                // creating a different genesis block:
                uint256 hashTarget = CBigNum().SetCompact(block.nBits).getuint256();
                uint256 thash;
               char scratchpad[SCRYPT_SCRATCHPAD_SIZE];

               loop
                {
                   scrypt_1024_1_1_256_sp(BEGIN(block.nVersion), BEGIN(thash), scratchpad);
                   if (thash <= hashTarget)
                       break;
                    if ((block.nNonce & 0xFFF) == 0)
                    {
                        printf("nonce %08X: hash = %s (target = %s)\n", block.nNonce, thash.ToString().c_str(), hashTarget.ToString().c_str());
                    }
                    ++block.nNonce;
                    if (block.nNonce == 0)
                    {
                        printf("NONCE WRAPPED, incrementing time\n");
                       ++block.nTime;
                    }
                }
                printf("block.nTime = %u  \n", block.nTime);
                printf("block.nNonce = %u \n", block.nNonce);
                printf("block.GetHash = %s\n", block.GetHash().ToString().c_str());

                }

            block.print();
            assert(hash == hashGenesisBlock);

            // Start new block file
            try {
                unsigned int nBlockSize = ::GetSerializeSize(block, SER_DISK, CLIENT_VERSION);
                CDiskBlockPos blockPos;
                CValidationState state;
                if (!FindBlockPos(state, blockPos, nBlockSize+8, 0, block.nTime))
                    return error("LoadBlockIndex() : FindBlockPos failed");
                if (!block.WriteToDisk(blockPos))
                    return error("LoadBlockIndex() : writing genesis block to disk failed");
                if (!block.AddToBlockIndex(state, blockPos))
                    return error("LoadBlockIndex() : genesis block not accepted");
            } catch(std::runtime_error &e) {
                return error("LoadBlockIndex() : failed to initialize block database: %s", e.what());
            }
        }

        return true;
    }

```

After this compile the code:
```
$cd src
$make -f makefile.unix
```

After the successful compilation altcoind file  get created inside ./src folder (daemon file).
Now run the altcoin blockchain using following command :
```
$cd src
$./altcoind -daemon
```
This error message will be display on console:
```
altcoind: main.cpp:2809: bool InitBlockIndex(): Assertion block.hashMerkleRoot == uint256("0x97ddfbbae6be97fd6cdf3e7ca13232a3afff2353e29badfab7f73011edd4ced9")' failed.
Aborted (core dumped).
```


Now redirect to .altcoin(inside home directory) folder and do the following (.altcoin is a local storage directory for public blockchain.)
```
$cd
$cd .altcoin
$sudo vim debug.log
```

Go at the end of this file see the following logs .


DEBUG.LOG :


```
2017-11-04 10:28:20 CBlock(hash=904fa8c7cc7efdce50d56015782b0c0ee80db19945023c9effa4def9a05503ae, input=01000000000000000000000000000000000000000000000000000000000000000000000040fb8c677b7eae579e4e3301db80e613538b2666ede265188bbfad2ce319a002b9aa8e4ef0ff0f1e8a35417c, PoW=000009b27c5889b83074c412d18e61585b88d5ac12210c32aa053e8fd4ae5f1c, ver=1, hashPrevBlock=0000000000000000000000000000000000000000000000000000000000000000, hashMerkleRoot=02a019e32cadbf8b1865e2ed66268b5313e680db01334e9e57ae7e7b678cfb40, nTime=1317972665, nBits=1e0ffff0, nNonce=2084648330, vtx=1)

```


  Now change following parameters inside  InitBlockIndex() function in src/main.cpp.


- Change parameter value of block.nNonce with DEBUG.LOG  nNonce for mainnet(https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.cpp#L2796). <br/>
- Uncomment assert(block.hashMerkleRoot == uint256("0x97ddfbbae6be97fd6cdf3e7ca13232a3afff2353e29badfab7f73011edd4ced9"));
and inside  uint256("0x") pass new   Merkle Root hash value  which is   DEBUG.LOG  "hashMerkleRoot" (e.g: assert(block.hashMerkleRoot == uint256("0x02a019e32cadbf8b1865e2ed66268b5313e680db01334e9e57ae7e7b678cfb40")); )
(https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.cpp#L2809)<br/>
- Replace  uint256 hashGenesisBlock("0x12a765e31ffd4059bada1e25190f6e98c99d9714d334efa41a195a7e7e04bfe2") tx hash value with DEBUG.LOG  "hash"  value (e.g: uint256 hashGenesisBlock("0x904fa8c7cc7efdce50d56015782b0c0ee80db19945023c9effa4def9a05503ae");) (https://github.com/litecoin-project/litecoin/blob/9cffb23c2d48d47bb67df78ea1164738b41e8c9d/src/main.cpp#L38)<br/>
-Remove POWCODE code from main.cpp file
-Recompile file using following commands.
```
$cd src 
$make -f makefile.unix
$./altcoind -daemon
```


Now this error message will be display on console:

```
Error: To use altcoind, you must set a rpcpassword in the configuration file:
/home/username/.altcoin/altcoin.conf
It is recommended you use the following random password:
rpcuser=altcoinrpc
rpcpassword=HbnwJiGVL4Nw8gYjtyRT84hLSFwndUFFvDBkTXJf2Njw
(you do not need to remember this password)
The username and password MUST NOT be the same.
If the file does not exist, create it with owner-readable-only file permissions.
It is also recommended to set alertnotify so you are notified of problems;
for example: alertnotify=echo %s | mail -s "Altcoin Alert" admin@foo.com
```

To fix this do the next step.


#### 16. Create a altcoin.conf file inside /home/username/.altcoin/
```
rpcuser=Yourusername
rpcpassword=Yourpassword
addnode=192.168.0.1
```

#### 17. To enable JSON-RPC commands, add `server = 1` in .conf file

#### 18. To run the test network, add `testnet = 1` in .conf file

#### 19. Add the another node using  `addnode=<ip>` in .conf file 

#### 20. Start mining using following command after starting daemon.
```
$./altcoind setgenerate true
```
