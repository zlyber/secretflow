# Zero-knowledge Proof (ZKP)

![](https://badgen.net/badge/:update-to/:Apr-2023/red) ![](https://badgen.net/badge/:papers/:92/blue) 


> **"We are currently experiencing a Cambrian Explosion in the field of cryptographic proofs of computational integrity (CI), a subset of which include zero knowledge proofs**. While a couple of years ago there were about 1–3 new systems a year, the rate has picked up so much that today we are seeing this same amount monthly, if not weekly."  
> 
> -- ELI BEN-SASSON, [A Cambrian Explosion of Crypto Proofs](https://nakamoto.com/cambrian-explosion-of-crypto-proofs/)

Since its invention in 1986, ZKP systems, more and more,  become building blocks for many other important domains, such as blockchains, Anonymous Credentials (in Web3), authentication systems, etc. In the following, we will mainly elaborate on the pratical ZKPs and roughly divide them into two categories: specific purpose ZKP and general purpose ZKP, in which their differences mainly come from the ability to prove different statements.
> If we compare this with Partial Homomorphic Encryption and Fully Homomorphic Encryption, specific ZKP can only prove some specific(simple) and finite statements, while general ZK (theoretically) can prove any statements.

- [Zero-knowledge Proof (ZKP)](#zero-knowledge-proof-zkp)
  - [Survey \& Tutorial](#survey--tutorial)
  - [Milestones](#milestones)
  - [Specific ZKP](#specific-zkp)
    - [Traditional \& simple relations (over logarithm)](#traditional--simple-relations-over-logarithm)
    - [Membership(Range) Proof](#membershiprange-proof)
  - [General purpose ZKP](#general-purpose-zkp)
    - [Frameworks](#frameworks)
    - [with SRS(Structured Reference String)](#with-srsstructured-reference-string)
    - [with updatable universal SRS](#with-updatable-universal-srs)
    - [with URS(Uniform Reference String)](#with-ursuniform-reference-string)
      - [DL-based](#dl-based)
      - [VOLE-based (Commit-and-prove type)](#vole-based-commit-and-prove-type)
    - [ZKSNARKS]
      - [Survey \& Tutorial]
      - [Theory]
      - [Implementation]
    - [STARKS]
  - [ZKP Standard Efforts](#zkp-standard-efforts)
  - [Applications on ZKP systems](#applications-on-zkp-systems)

## Survey & Tutorial

- Zero-Knowledge twenty years after its invention, also called A Short Tutorial of Zero-Knowledge  
  *Oded Goldreich*  
  Gol10, [paper](https://www.wisdom.weizmann.ac.il/~oded/PSX/zk-tut10.pdf), [Gol04 older version](https://www.wisdom.weizmann.ac.il/~oded/PSX/zk-tut02v4.pdf),[homepage](https://www.wisdom.weizmann.ac.il/~oded/zk-tut02.html)

## Milestones

- The Knowledge Complexity of Interactive Proof-Systems (**Invention of zero-knowledge**)  
  *Shafi Goldwasser, Silvio Micali, and Charle Rackoff*  
  STOC 1985, [paper](https://dl.acm.org/doi/10.1145/22145.22178), GMR85

- On defining proofs of knowledge  
  *Bellare Mihir and Oded Goldreich*  
  CRYPTO 1992, [paper](https://link.springer.com/chapter/10.1007/3-540-48071-4_28), BG92

- Efficient Identification and Signatures for Smart Cards  
  *Schnorr Claus-Peter*  
  CRYPTO 1989, [paper](https://link.springer.com/chapter/10.1007/0-387-34805-0_22), Sch89

- Short Pairing-Based Non-Interactive Zero-Knowledge Arguments  
  *Groth Jens*  
  ASIACRYPT 2010, [paper](http://www0.cs.ucl.ac.uk/staff/J.Groth/ShortNIZK.pdf), Gro10

- Quadratic Span Programs and Succinct NIZKs without PCPs  
  *Rosario Gennaro, Craig Gentry, Bryan Parno, and Mariana Raykova*  
  EUROCRYPT 2013, [paper](https://eprint.iacr.org/2012/215), GGPR13

- On the Size of Pairing-Based Non-Interactive Arguments  
  *Groth Jens*  
  EUROCRYPT 2016, [paper](https://eprint.iacr.org/2016/260), Gro16

- Bulletproofs: Short Proofs for Confidential Transactions and More  
  *Benedikt Bunz, Jonathan Bootle, Dan Boneh, Andrew Poelstra, Pieter Wuille, and Greg Maxwell*  
  S&P 2018, [paper](https://eprint.iacr.org/2017/1066), BBB+18

- PLONK: Permutations over Lagrange-Bases for Oecumenical Noninteractive Arguments of Knowledge  
  *Ariel Gabizon, Zachary J. Williamson, and Oana Ciobotaru*  
  eprint 2019, [paper](https://eprint.iacr.org/2019/953), GWC19

- Wolverine: Fast, Scalable, and Communication-Efficient Zero-Knowledge Proofs for Boolean and Arithmetic Circuits  
  *Chenkai Weng, Kang Yang, Jonathan Katz, and Xiao Wang*  
  S&P 2021, [paper](https://eprint.iacr.org/2020/925), WYK+21

## Specific ZKP

### Traditional & simple relations (over logarithm)

- Efficient Identification and Signatures for Smart Cards  
  *Claus-Peter Schnorr*  
  CRYPTO 1989, [paper](https://link.springer.com/chapter/10.1007/0-387-34805-0_22), Sch89

- A Practical Zero-Knowledge Protocol Fitted to Security Microprocessor Minimizing Both Transmission and Memory  
  *Louis C. Guillou, and Jean-Jacques Quisquater*  
  EUROCRYPT 1988, [paper](http://link.springer.com/10.1007/3-540-45961-8_11), GQ88

- Proofs of Partial Knowledge and Simplified Design of Witness Hiding Protocols  
  *Ronald Cramer, Ivan Damgård, and Berry Schoenmakers*  
  CRYPTO 1994, [paper](https://link.springer.com/chapter/10.1007/3-540-48658-5_19), CDS94

- Proof Systems for General Statements about Discrete Logarithms  
  *Jan Camenisch, and Markus Stadler*  
  ETH Zurich Report 1997, [paper](https://www.research-collection.ethz.ch/handle/20.500.11850/69316), CS97

- Short Group Signatures  
  *Dan Boneh, Xavier Boyen, and Hovav Shacham*  
  CRYPTO 2004, [paper](https://eprint.iacr.org/2004/174), BBS04

- Unifying Zero-Knowledge Proofs of Knowledge  
  *Maurer Ueli*  
  AFRICACRYPT 2009, [paper](https://link.springer.com/chapter/10.1007/978-3-642-02384-2_17), Mau09

- Non-Interactive Composition of Sigma-Protocols via Share-Then-Hash  
  *Masayuki Abe, Miguel Ambrona, Andrej Bogdanov, Miyako Ohkubo, and Alon Rosen*  
  ASIACRYPT 2020, [paper](https://eprint.iacr.org/2021/457), AAB+20

- Compressing Proofs of K-Out-Of-n Partial Knowledge  
  *Thomas Attema, Ronald Cramer, and Serge Fehr*  
  CRYPTO 2021, [paper](https://eprint.iacr.org/2020/753), ACF21

- DAG-Sigma: A DAG-Based Sigma Protocol for Relations in CNF  
  *Gongxian Zeng, Junzuo Lai, Zhengan Huang, Yu Wang, and Zhiming Zheng*  
  ASIACRYPT 2022, [paper](https://eprint.iacr.org/2022/1569), ZLH+22

- Revisiting BBS Signatures  
  *Stefano Tessaro and Chenzhi Zhu*  
  EUROCRYPT 2023, [paper](https://eprint.iacr.org/2023/275), TZ23

### Membership(Range) Proof

- A Digital Signature Based on a Conventional Encryption Function  
  *Ralph C Merkle*  
  CRYPTO 1987, [paper](https://link.springer.com/chapter/10.1007/3-540-48184-2_32), Mer87

- Statistical Zero Knowledge Protocols to Prove Modular Polynomial Relations  
  *Eiichiro Fujisaki, and Tatsuaki Okamoto*  
  CRYPTO 1997, [paper](https://link.springer.com/chapter/10.1007/BFb0052225), FO97

- Efficient proofs that a committed number lies in an interval  
  *Fabrice Boudot*  
  EUROCRYPT 2000, [paper](https://link.springer.com/chapter/10.1007/3-540-45539-6_31), Bou00

- Dynamic Accumulators and Application to Efficient Revocation of Anonymous Credentials  
  *Jan Camenisch and Anna Lysyanskaya*  
  CRYPTO 2002, [paper](https://link.springer.com/chapter/10.1007/3-540-45708-9_5), CL02

- Accumulators from Bilinear Pairings and Applications to ID-Based Ring Signatures and Group Membership Revocation  
  *Nguyen Lan*  
  CT-RSA 2005, [paper](https://eprint.iacr.org/2005/123), Ngu05

- Efficient Protocols for Set Membership and Range Proofs  
  *Jan Camenisch, Rafik Chaabouni, and abhi shelat*  
  ASIACRYPT 2008, [paper](https://link.springer.com/chapter/10.1007/978-3-540-89255-7_15), CCs08

- An Accumulator Based on Bilinear Maps and Efficient Revocation for Anonymous Credentials  
  *Jan Camenisch, Markulf Kohlweiss, and Claudio Soriente*  
  PKC 2009, [paper](https://eprint.iacr.org/2008/539), CKS09

- Bulletproofs: Short Proofs for Confidential Transactions and More  
  *Benedikt Bunz, Jonathan Bootle, Dan Boneh, Andrew Poelstra, Pieter Wuille, and Greg Maxwell*  
  S&P 2018, [paper](https://eprint.iacr.org/2017/1066), BBB+18

- Batching Techniques for Accumulators with Applications to IOPs and Stateless Blockchains  
  *Dan Boneh, Benedikt Bünz, and Ben Fisch*  
  CRYPTO 2019, [paper](https://eprint.iacr.org/2018/1188), BBF19

- Compressed $\varSigma$-Protocol Theory and Practical Application to Plug & Play Secure Algorithmics  
  *Thomas Attema, and Ronald Cramer*  
  CRYPTO 2020, [paper](https://eprint.iacr.org/2020/152), AC20

- Caulk: Lookup Arguments in Sublinear Time  
  *Arantxa Zapico, Vitalik Buterin, Dmitry Khovratovich, Mary Maller, Anca Nitulescu, and Mark Simkin*  
  CCS21, [paper](https://eprint.iacr.org/2022/621), ZBK+21

- Zero-Knowledge Proofs for Set Membership: Efficient, Succinct, Modular  
  *Daniel Benarroch, Matteo Campanelli, Dario Fiore, Kobi Gurkan, and Dimitris Kolonelos*  
  FC 2021, [paper](https://eprint.iacr.org/2019/1255), BGF+21

- Batching, Aggregation, and Zero-Knowledge Proofs in Bilinear Accumulators  
  *Shravan Srinivasan, Ioanna Karantaidou, Foteini Baldimtsi, and Charalampos Papamanthou*  
  CCS 2022, [paper](https://eprint.iacr.org/2022/1779), SKB+22

- Succinct Zero-Knowledge Batch Proofs for Set Accumulators  
  *Matteo Campanelli, Dario Fiore, Semin Han, Jihye Kim, Dimitris Kolonelos, and Hyunok Oh*  
  CCS 2022, [paper](https://eprint.iacr.org/2021/1672), CFH+22

## General purpose ZKP

### Frameworks

- Interactive Oracle Proofs  
  *Eli Ben-Sasson, Alessandro Chiesa, and Nicholas Spooner*  
  TCC 2016, [paper](https://eprint.iacr.org/2016/116), BCS16

- Spartan: Efficient and General-Purpose ZkSNARKs Without Trusted Setup  
  *Srinath Setty*  
  CRYPTO 2020, [paper](https://eprint.iacr.org/2019/550), Set20

- VOProof: Efficient ZkSNARKs from Vector Oracle Compilers  
  *Yuncong Zhang, Alan Szepeniec, Ren Zhang, Shi-Feng Sun, Geng Wang, and Dawu Gu*  
  CCS 2022, [paper](https://eprint.iacr.org/2021/710), ZSZ+22

### with SRS(Structured Reference String)

Traditional SRS usually need trusted setup per curcuit.

- Short Pairing-Based Non-Interactive Zero-Knowledge Arguments  
  *Groth Jens*  
  ASIACRYPT 2010, [paper](http://www0.cs.ucl.ac.uk/staff/J.Groth/ShortNIZK.pdf), Gro10

- Quadratic Span Programs and Succinct NIZKs without PCPs  
  *Rosario Gennaro, Craig Gentry, Bryan Parno, and Mariana Raykova*  
  EUROCRYPT 2013, [paper](https://eprint.iacr.org/2012/215), GGPR13

- On the Size of Pairing-Based Non-Interactive Arguments  
  *Groth Jens*  
  EUROCRYPT 2016, [paper](https://eprint.iacr.org/2016/260), Gro16

- DIZK: A Distributed Zero Knowledge Proof System  
  *Howard Wu, Wenting Zheng, Alessandro Chiesa, Raluca Ada Popa, and Ion Stoica*  
  USENIX 2018, [paper](https://eprint.iacr.org/2018/691), WZC+18

- Snarky Ceremonies  
  *Markulf Kohlweiss, Mary Maller, Janno Siim, and Mikhail Volkhov*  
  ASIACRYPT 2021, [paper](https://eprint.iacr.org/2021/219), KMS+21

### with updatable universal SRS

Updatable universal SRS means that the same SRS by a trusted setup could be used for statements about all circuits of a certain bounded size.

- Sonic: Zero-Knowledge SNARKs from Linear-Size Universal and Updatable Structured Reference Strings  
  *Mary Maller, Sean Bowe, Markulf Kohlweiss, and Sarah Meiklejohn*  
  CCS 2019, [paper](https://eprint.iacr.org/2019/099), MBK+19

- Marlin: Preprocessing ZkSNARKs with Universal and Updatable SRS  
  *Alessandro, Chiesa, Yuncong Hu, Mary Maller, Pratyush Mishra, Noah Vesely, and Nicholas Ward*  
  EUROCRYPT 2020, [paper](https://eprint.iacr.org/2019/1047), CHM+20

- PLONK: Permutations over Lagrange-Bases for Oecumenical Noninteractive Arguments of Knowledge  
  *Ariel Gabizon, Zachary J. Williamson, and Oana Ciobotaru*  
  eprint 2019, [paper](https://eprint.iacr.org/2019/953), GWC19

- MIRAGE: Succinct Arguments for Randomized Algorithms with Applications to Universal Zk-SNARKs  
  *Ahmed Kosba, Dimitrios Papadopoulos, Charalampos Papamanthou, and Dawn Song*  
  USENIX Security 2020, [paper](https://eprint.iacr.org/2020/278), KPP+20

- Lunar: A Toolbox for More Efficient Universal and Updatable ZkSNARKs and Commit-and-Prove Extensions  
  *Matteo Campanelli, Antonio Faonio, Dario Fiore, Anaïs Querol, and Hadrián Rodríguez*  
  ASIACRYPT 2021, [paper](https://eprint.iacr.org/2020/1069), CFF+21

- An Algebraic Framework for Universal and Updatable SNARKs  
  *Carla Ràfols, and Arantxa Zapico*  
  CRYPTO 2021, [paper](https://eprint.iacr.org/2021/590), RZ21

- Counting Vampires: From Univariate Sumcheck to Updatable ZK-SNARK  
  *Helger Lipmaa, Janno Siim, and Michał Zając*  
  ASIACRYPT 2022, [paper](https://eprint.iacr.org/2022/406), LSZ22

### with URS(Uniform Reference String)

Without trusted setup.

- Ligero: Lightweight Sublinear Arguments Without a Trusted Setup  
  *Scott Ames, Carmit Hazay, Yuval Ishai, and Muthuramakrishnan Venkitasubramaniam*  
  CCS 2017, [paper](https://eprint.iacr.org/2022/1608), AHI+17

- Scalable Zero Knowledge with No Trusted Setup  
  *Eli Ben-Sasson, Iddo Bentov, Yinon Horesh, and Michael Riabzev*  
  CRYPTO 2019, [paper](https://www.iacr.org/archive/crypto2019/116940201/116940201.pdf), BBH+19

- Aurora: Transparent Succinct Arguments for R1CS  
  *Eli Ben-Sasson, Alessandro Chiesa, Michael Riabzev, Nicholas Spooner, Madars Virza, and Nicholas P. Ward*  
  EUROCRYPT 2019, [paper](https://eprint.iacr.org/2018/828), BCR+19

- Ligero++: A New Optimized Sublinear IOP  
  *Rishabh Bhadauria, Zhiyong Fang, Carmit Hazay, Muthuramakrishnan Venkitasubramaniam, Tiancheng Xie, and Yupeng Zhang*  
  CCS 2020, [paper](https://dl.acm.org/doi/10.1145/3372297.3417893), BFH+20

- Fractal: Post-Quantum and Transparent Recursive Proofs from Holography  
  *Alessandro Chiesa, Dev Ojha, and Nicholas Spooner*  
  EUROCRYPT 2020, [paper](https://eprint.iacr.org/2019/1076), COS20

- Transparent Polynomial Delegation and Its Applications to Zero Knowledge Proof  
  *Jiaheng Zhang, Tiancheng Xie, Yupeng Zhang, and Dawn Song*  
  S&P 2020, [paper](https://eprint.iacr.org/2019/1482), ZXZ+20

- Sumcheck Arguments and Their Applications  
  *Jonathan Bootle, Alessandro Chiesa, and Katerina Sotiraki*  
  CRYPTO 2021, [paper](https://eprint.iacr.org/2021/333), BCS21

- RedShift: Transparent SNARKs from List Polynomial Commitments  
  *Assimakis A. Kattis, Konstantin Panarin, and Alexander Vlasov*  
  CCS 2022, [paper](https://eprint.iacr.org/2019/1400), KPV22

- Flashproofs: Efficient Zero-Knowledge Arguments of Range and Polynomial Evaluation with Transparent Setup  
  *Nan Wang, and Sid Chi-Kin Chau*  
  ASIACRYPT 2022, [paper](https://eprint.iacr.org/2022/1251), WC22

#### DL-based

- Efficient Zero-Knowledge Arguments for Arithmetic Circuits in the Discrete Log Setting  
  *Jonathan Bootle, Andrea Cerulli, Pyrros Chaidos, Jens Groth, and Christophe Petit*  
  EUROCRYPT 2016, [paper](https://eprint.iacr.org/2016/263), BCC+16

- Doubly-Efficient ZkSNARKs Without Trusted Setup  
  *Riad S. Wahby, Ioanna Tzialla, Abhi Shelat, Justin Thaler, and Michael Walfish*  
  SP 2018, [paper](https://eprint.iacr.org/2017/1132), WTS+18

- Bulletproofs: Short Proofs for Confidential Transactions and More  
  *Benedikt Bunz, Jonathan Bootle, Dan Boneh, Andrew Poelstra, Pieter Wuille, and Greg Maxwell*  
  S&P 2018, [paper](https://eprint.iacr.org/2017/1066), BBB+18

- Non-Interactive Zero-Knowledge Proofs for Composite Statements  
  *Shashank Agrawal, Chaya Ganesh, and Payman Mohassel*  
  CRYPTO 2018, [paper](https://eprint.iacr.org/2018/557), AGM18

- Shorter Non-Interactive Zero-Knowledge Arguments and ZAPs for Algebraic Languages  
  *Geoffroy Couteau, and Dominik Hartmann*  
  CRYPTO 2020, [paper](https://eprint.iacr.org/2020/286), CH20

- Compressed $\varSigma$-Protocol Theory and Practical Application to Plug & Play Secure Algorithmics  
  *Thomas Attema, and Ronald Cramer*  
  CRYPTO 2020, [paper](https://eprint.iacr.org/2020/152), AC20
  
- Compressed $\varSigma$-Protocols for Bilinear Group Arithmetic Circuits and Application to Logarithmic Transparent Threshold Signatures  
  *Thomas Attema, Ronald Cramer, and Matthieu Rambaud*  
  ASIACRYPT 2021, [paper](https://eprint.iacr.org/2020/1447), ACR21

- Halo Infinite: Proof-Carrying Data from Additive Polynomial Commitments  
  *Dan Boneh, Justin Drake, Ben Fisch, and Ariel Gabizon*  
  CRYPTO 2021, [paper](https://eprint.iacr.org/2020/1536), BDF+21

- Efficient NIZKs for Algebraic Sets  
  *Geoffroy Couteau, Helger Lipmaa, Roberto Parisella, and Arne Tobias Ødegaard*  
  ASIACRYPT 2021, [paper](https://eprint.iacr.org/2021/1251), CLP+21

- ECLIPSE: Enhanced Compiling Method for Pedersen-Committed ZkSNARK Engines  
  *Diego F. Aranha, Emil Madsen Bennedsen, Matteo Campanelli, Chaya Ganesh, Claudio Orlandi, and Akira Takahashi*  
  PKC 2022, [paper](https://eprint.iacr.org/2021/934), ABC+22

#### VOLE-based (Commit-and-prove type)

- Appenzeller to Brie: Efficient Zero-Knowledge Proofs for Mixed-Mode Arithmetic and Z2k  
  *Carsten Baum, Lennart Braun, Alexander Munch-Hansen, Benoit Razet, and Peter Scholl*  
  CCS 2021, [paper](https://eprint.iacr.org/2021/750), BBM+21

- $\mathsf{Mac’n’Cheese}$: Zero-Knowledge Proofs for Boolean and Arithmetic Circuits with Nested Disjunctions  
  *Carsten Baum, Alex J. Malozemoff, Marc B. Rosen, and Peter Scholl*  
  CRYPTO 2021, [paper](https://eprint.iacr.org/2020/1410), BMR+21

- Line-Point Zero Knowledge and Its Applications  
  *Samuel Dittmer, Yuval Ishai, and Rafail Ostrovsky*  
  ITC 2021, [paper](https://eprint.iacr.org/2020/1446), DIO21

- Wolverine: Fast, Scalable, and Communication-Efficient Zero-Knowledge Proofs for Boolean and Arithmetic Circuits  
  *Chenkai Weng, Kang Yang, Jonathan Katz, and Xiao Wang*  
  S&P 2021, [paper](https://eprint.iacr.org/2020/925), WYK+21

- QuickSilver: Efficient and Affordable Zero-Knowledge Proofs for Circuits and Polynomials over Any Field  
  *Kang Yang, Pratik Sarkar, Chenkai Weng, and Xiao Wang*  
  CCS 2021, [paper](https://eprint.iacr.org/2021/076), YSW+21

- Mystique: Efficient Conversions for Zero-Knowledge Proofs with Applications to Machine Learning  
  *Chenkai Weng, Kang Yang, Xiang Xie, Jonathan Katz, and Xiao Wang*  
  USENIX 2021. [paper](https://eprint.iacr.org/2021/730), WYX+21

- Improving Line-Point Zero Knowledge: Two Multiplications for the Price of One  
  *Samuel Dittmer, Yuval Ishai, Steve Lu, and Rafail Ostrovsky*  
  CCS 2022, [paper](https://eprint.iacr.org/2022/552), DIL+22

- AntMan: Interactive Zero-Knowledge Proofs with Sublinear Communication  
  *Chenkai Weng, Kang Yang, Zhaomin Yang, Xiang Xie, and Xiao Wang*  
  CCS 2022, [paper](https://eprint.iacr.org/2022/566), WYY+22

### ZKSNARKS

#### Survey&Tutorial

- zk-SNARKs: A Gentle Introduction
  *Anca Nitulescu*
  [paper](https://www.di.ens.fr/~nitulesc/files/Survey-SNARKs), 2020
 
- zkSNARKs in a nutshell
  *Christian Reitwiessner*
  Ethereum blog 2016, [blog](https://www.di.ens.fr/~nitulesc/files/Survey-SNARKs)
 
#### Theory

- Quadratic Span Programs and Succinct NIZKs without PCPs  
  *Rosario Gennaro, Craig Gentry, Bryan Parno, and Mariana Raykova*  
  EUROCRYPT 2013, [paper](https://eprint.iacr.org/2012/215), GGPR13
  
- From extractable collision resistance to succinct non-interactive arguments of knowledge, and back again
 *Nir Bitansky, Ran Canetti, Alessandro Chiesa, and Eran Tromer*
  ITCS 2012, [paper](https://eprint.iacr.org/2011/443), BCC+12
 
- Succinct Non-Interactive Zero Knowledge for a von Neumann Architecture
 *Eli Ben-Sasson, Alessandro Chiesa, Eran Tromer, and Madars Virza*
  USENIX Security 2014, [paper](https://eprint.iacr.org/2013/879), BCT+14
  
- On the Size of Pairing-Based Non-Interactive Arguments  
  *Groth Jens*  
  EUROCRYPT 2016, [paper](https://eprint.iacr.org/2016/260), Gro16

- PLONK: Permutations over Lagrange-Bases for Oecumenical Noninteractive Arguments of Knowledge  
  *Ariel Gabizon, Zachary J. Williamson, and Oana Ciobotaru*  
  eprint 2019, [paper](https://eprint.iacr.org/2019/953), GWC19
  
- Halo: Recursive Proof Composition without a Trusted Setup
 *Sean Bowe, Jack Grigg, and Daira Hopwood*
  eprint 2019, [paper](https://eprint.iacr.org/2019/1021), BGH19

#### Implementation

- PipeZK: Accelerating Zero-Knowledge Proof with a Pipelined Architecture
 *Ye Zhang, Shuo Wang, Xian Zhang, Jiangbin Dong, Xingzhong Mao, Fan Long, Cong Wang, Dong Zhou, Mingyu Gao, and Guangyu Sun*
  ISCA 2021, [paper](https://www.microsoft.com/en-us/research/uploads/prod/2021/05/isca21_pizk-60a269dbb1310), ZWZ+21
  
- GZKP: A GPU Accelerated Zero-Knowledge Proof System
 *Weiliang Ma, Qian Xiong, Xuanhua Shi, Xiaosong Ma, Haici Jin, Haozhao Kuang, M. Gao, Ye Zhang, Haichen Shen, and Weifang Hu*
  ASPLOS 2023, [paper](https://dl.acm.org/doi/10.1145/3575693.3575711), MXS+23
  
### STARKS
- Scalable, transparent, and post-quantum secure computational integrity
  *Eli Ben-Sasson, Iddo Bentov, Y. Horesh, and Michael Riabzev*
  eprint 2018, [paper](https://eprint.iacr.org/2018/046), BBH+18
  
- DEEP-FRI: Sampling outside the box improves soundness
  *Eli Ben-Sasson, Lior Goldberg, Swastik Kopparty, Shubhangi Saraf*
  eprint 2019, [paper](https://eprint.iacr.org/2019/336), BGK+19
  
- Proximity Gaps for Reed–Solomon Codes
  *Eli Ben-Sasson, Dan Carmon, Y. Ishai, Swastik Kopparty, Shubhangi Saraf*
  FOCS 2020, [paper](https://ieeexplore.ieee.org/document/9317990), BCI+20

## ZKP Standard Efforts


- RFC: Schnorr Non-Interactive Zero-Knowledge Proof  
  *Hao, Feng*  
  IETF rfc8235, [paper](https://datatracker.ietf.org/doc/rfc8235), Hao 21

Below are from organization [zkproof](https://zkproof.org/):
> ZKProof is an open-industry academic initiative that seeks to mainstream zero-knowledge proof (ZKP) cryptography through an inclusive, community-driven standardization process that focuses on interoperability and security.

- Proposal: Commit-and-Prove Zero-Knowledge Proof Systems and Extensions  
  *Daniel Benarroch, Matteo Campanelli, Dario Fiore, Jihye Kim, Jiwon Lee, Hyunok Oh, and Anaıs Querol*  
  ZKProof 2,3,4th workshop, [paper](https://docs.zkproof.org/pages/standards/accepted-workshop4/proposal-commit.pdf), BCF+21

- Rinocchio: SNARKs for Ring Arithmetic  
  *Ganesh, Chaya, Anca Nitulescu, and Eduardo Soria-Vazquez*  
  ZKProof 4th workshop, 2021, [paper](https://docs.zkproof.org/pages/standards/accepted-workshop4/proposal-rinocchio.pdf)

- Zk-Proof Community——Proposal: Σ-Protocols  
  *Stephan Krenn and Michele Orrù*  
  ZKProof 4th workshop, 2021, [paper](https://docs.zkproof.org/pages/standards/accepted-workshop4/proposal-sigma.pdf), KO21

- See more at [zkproof proposals](https://docs.zkproof.org/standards/proposals).


## Applications on ZKP systems

Here just list several interesting applicaitons.

- Constant-Size Dynamic k-Tatsuaki  
  *Man Ho Au, Willy Susilo, and Yi Mu*  
  SCN06, [paper](https://eprint.iacr.org/2008/136), ASM06

- Anonymous Credentials Light  
  *Foteini Baldimtsi, and Anna Lysyanskaya*  
  CCS 2013, [paper](https://eprint.iacr.org/2012/298), BL13

- Anonymous Attestation Using the Strong Diffie Hellman Assumption Revisited  
  *Jan Camenisch, Manu Drijvers, and Anja Lehmann*  
  Trust and Trustworthy Computing 2016, [paper](https://eprint.iacr.org/2016/663), CDL16

- Scaling Veriﬁable Computation Using Efﬁcient Set Accumulators  
  *Alex Ozdemir, Riad S Wahby, Barry Whitehat, and Dan Boneh*  
  USENIX 2020, [paper](https://www.usenix.org/conference/usenixsecurity20/presentation/ozdemir), OWW+20

- Zero Knowledge Proofs for Decision Tree Predictions and Accuracy  
  *Jiaheng Zhang, Zhiyong Fang, Yupeng Zhang, and Dawn Song*  
  CCS 2020. [paper](https://dl.acm.org/doi/10.1145/3372297.3417278), ZFZ+20

- DECO: Liberating Web Data Using Decentralized Oracles for Threshold  
  *Fan Zhang, Sai Krishna Deepak Maram, Harjasleen Malvai, Steven Goldfeder, and Ari Juels*  
  CCS 2020, [paper](https://dl.acm.org/doi/10.1145/3372297.3417239), ZMM+20

- ZkCNN: Zero Knowledge Proofs for Convolutional Neural Network Predictions and Accuracy  
  *Tianyi Liu, Xiang Xie, and Yupeng Zhang*  
  CCS 2021, [paper](https://eprint.iacr.org/2021/673), LXZ21

- ZeeStar: Private Smart Contracts by Homomorphic Encryption and Zero-Knowledge Proofs  
  *Samuel Steffen, Benjamin Bichsel, Roger Baumgartner, and Martin Vechev*  
  S&P 2022, [paper](https://files.sri.inf.ethz.ch/website/papers/sp22-zeestar.pdf), SBB+22

- Zero-Knowledge Middleboxes  
  *Paul Grubbs, Arasu Arun, Ye Zhang, Joseph Bonneau, and Michael Walfish*  
  USENIX 2022, [paper](https://eprint.iacr.org/2021/1022), GAZ+22

- Zk-Creds: Flexible Anonymous Credentials from ZkSNARKs and Existing Identity Infrastructure  
  *Michael Rosenberg, Jacob White, Christina Garman, and Ian Miers*  
  S&P 2023, [paper](https://eprint.iacr.org/2022/878), RWG+23
