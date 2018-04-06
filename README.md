# Gladius Coding Challenge

Welcome to the Gladius coding challenge. The challenge is pretty simple, create a dApp (Decentralized App) that submits your hiring information (encrypted against our public key) to the blockchain.

## Overview

Blockchain development is relatively new, so we've created this challenge in a way that there are multiple levels of completion. We are looking for creativity and problem solving skills are more important than 100% completion.

This challenge asks that you write a server side application with a client facing blockchain interface, for instance Node.js with Express routing; an interface to input data to submit; and successfully submitting this data to our deployed contract. This can be done client sided where the user authorizes transactions through something like MetaMask.

Our contract has been deployed to the Ropsten Test Net. If you need the Application Contract address, email us at [careers@gladius.io](mailto://careers@gladius.io). We want to keep this secret to get an estimate of time to completion.

You will have approximately 2 days to complete and submit your application to the blockchain. We are not going to judge by time per se, e.g. a complete well-coded application that took 3 days is better than a rushed application that took a single day.

If anything comes up or you have questions, email us at [careers@gladius.io](mailto://careers@gladius.io).

## Contract Structure

Our Contract: Applications.sol

Getters:

```
// Returns the PGP Public Key used to encrypt your submission data against
getPublicKey() -> String

// Returns the Unencrypted data payload with instructions on what to post in submitApplication()
getPublicData() -> String

// Same as getPublicData, but includes a secret key. This is encrypted against the Public Key below
getEncryptedData() -> String

// After successfully submitting your application, input your address here to view your submission
getApplication(Address applicant) -> String
```

Functions:

```
// Function to submit your application payload.
// Takes in a String.
// We are looking for a JSON payload from getPublicData() or getEncryptedData()
// Reminder, any unencrypted data is public for anyone on the Ropsten chain, encrypt before submitting here
submitApplication(String applicationData)
```

## What We're Looking For

We will be judging submissions based on code quality, completeness, and time to completion within reason. The main qualities we look for are resourcefulness and the desire to learn / try new technology.

Levels of Completion and Tasks to Complete:

* Level 1
  * Create a server side application to serve the webpage
  * This application or client is able to read `getPublicData()` from the Ropsten Network deployed contract, this is the specification of what should be sent later.
  * The client is able to show the above specification in the UI as a form.
* Level 2
  * Same as above plus...
  * Submits the above form to the `submitApplication(data)` function in the contract
* Level 3
  * Same as above plus...
  * Reads and decrypts the data specification from `getEncryptedData()` using your private key (at the bottom of this page)
  * Fill in the required fields in the UI.
  * Encrypt that data against the contract public key.
  * Submits this back to the contract through the `submitApplication(data)` function
* Level 4
  * Same as above plus...
  * Adds some form of originality and creativity to the UI
  * Adds ease of use
  * Pulls in and displays extra data from the limited data given
  * Any other criteria that shows going above and beyond

Your final project should be uploaded to a GitHub repository publicly. This can be a different user name than your personal user name. If this is an issue, reach out to us and we can take submissions in a different manner.

## General Steps

* Build an dApp to read an Ethereum contract property
* Decrypt or read the contract's data
  * The contract will contain two JSON payloads, one plain text and the other encrypted against the public key provided below
  * If encrypted, use the included private key to decrypt this message
  * The message will be a JSON specification with fields to include to submit to the contract
* Create a way to submit the correct data requested by the property's data
  * Using a REST client, e.g. POSTman, Insomnia, or web form
  * Web UI
* Submit the data encrypted against the contract's Public Key from `getPublicKey()`
* Upload project to GitHub with this information in the README
  * Application Address or txHash of the transaction from submitting data in the `submitApplication(data)` method

If at any point something is unclear or information is not provided, reach out and we can help. We would rather spend some time helping someone over having them blocked for hours on end.

Good Luck!!

## Resources

One of the most common wallet managers is [MetaMask](https://metamask.io/). Register and create a new account to get started. All of the transactions should take place on Ropsten Test Net. You will not need to put any real money into this. In MetaMask, switch to the Ropsten Test Net and hit the "Deposit" button. After, there is a button to access the faucet. This allows for free test ether deposits into your account. A direct link to the faucet is [here](https://faucet.metamask.io/).

For rapid development, we recommend using the [web3 js framework](https://github.com/ethereum/web3.js/) to access the blockchain.

Truffle has a great tutorial to use Infura to connect to the Ropsten test network [here](http://truffleframework.com/tutorials/using-infura-custom-provider)

A great utility to check statuses, errors, and txHashes: [etherscan](https://ropsten.etherscan.io/)

See the `Application Contract ABI` section of this gist for the Application Contract JSON Interface ABI.

To initialize the Contract in order to call methods, see the [web3 docs](https://web3js.readthedocs.io/en/1.0/web3-eth-contract.html#new-contract).

A quick js example is below
```javascript
let contract = new web3.eth.Contract(jsonInterface[, address][, options])
```

For encryption / decryption we are currently using [Keybase's PGP library](https://keybase.io/kbpgp)

### Application Contract ABI

Use this in the `web3.eth.Contract` constructor

See [Application-ABI.json
](https://github.com/gladiusio/gladius-hiring-challenge/blob/master/Application-ABI.json) for full JSON file.

### Keys

Below are keys to use in your dApp, we've encrypted some data on the blockchain against the public key below:

```
-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: Keybase OpenPGP v1.0.0
Comment: https://keybase.io/crypto

xo0EWsZSvQEEAOSjrTJNTnJd/eg9dWTY3Mlo/0ZS/sniamQCeGtwqVGD8LRaQlK6
f6zMN71hcttBeJbZd3HUNtFArU0tB8lkyKJQSaha+uWWYyqfZsF/3GaZ6I4UFT0z
w/KEPEvl3dPfamH34Ei3IQv+OThfFJHDslhP/wysCaAib121RJE33TmZABEBAAHN
IkdsYWRpdXMgSGlyZWUgPGNhcmVlcnNAZ2xhZGl1cy5pbz7CrQQTAQoAFwUCWsZS
vQIbLwMLCQcDFQoIAh4BAheAAAoJEDiZEtmr5GtAelUD/R9ndN0mYnMmPu4m5QUB
DYHeti5gf6vKDQtVS9tNs7xaDFW7G1OOsNUvTEHYzXNVWCHyD0lfqMouhX/yDr0F
vemYdRj5pyMDefjCHHz1sFsvz5dzTGr+0pyfKFVaKByKCs+IErTB9HcgmUIuZIiK
EJw0kNPRgqoujb/g/Zb9AG/xzo0EWsZSvQEEAMAU50K0XKJWqhVQlem6oCodfBza
u/0lX2T2BZlNrJcDr00NNPMjxBNKShEmP9a86FYHvAHRnAZsYqJT9rx4tEDNi8fE
ZwV2OlDensiQ2dpIICa7tpks2o1PMxy8bpzAiJeO42p9+BqgzRFGEQWT+PKEd/61
pm9kE31AVOL/x/DBABEBAAHCwIMEGAEKAA8FAlrGUr0FCQ8JnAACGy4AqAkQOJkS
2avka0CdIAQZAQoABgUCWsZSvQAKCRAe1HnTAAd/+B8nBAC7DBWZ7UEYqs0DctUy
CDfyncZJ3V2EAug3O7tBCYMM8/NY5ZsBCqR6Zbk8+fKeuYUX7uOuY9hwMxoz0D/D
HKLLtLSggEC2A8M1/QuAQXPeKbI08hIvHWvJbm4AXSY8ob+CjBxtc3LfxmswGocN
3pN7KYJTiHlIgzmTdQD2vnqZRMHfBACTGTW2ptXFMeYvfmsmq42B9cbRhTEM+/0u
onCCvDCz8OIw4Hd6EF8GFRQHObesim7XeUhZPMYK28ep5Gf8Qnwg94JdrYxaapO+
Ngdht9WheAPvlBa/yumgL9Jzm1rq2iHKZ5JWtDvJFPnQf3Q75Z+CXbSrHNcD4ETK
6smVlmWdJs6NBFrGUr0BBAC15JKl7Sc0O9WwcRe1tLe8sRul6O5pyGt0phSxZnWH
4iTCbSxjNvTPrPCxWr4a2yAajzxUojkvk9AfTiJ71Zr8WfCSHvYnBm5V3VVDnqh3
Rt5MnFk0S2G2CBgG78xXnQ4BfdXIJykJFEcWAxq9N/rxQDHfLsO91ejq0suY8E6O
AwARAQABwsCDBBgBCgAPBQJaxlK9BQkPCZwAAhsuAKgJEDiZEtmr5GtAnSAEGQEK
AAYFAlrGUr0ACgkQ3+HC5nwXrzZ2zQP/QJhBE/fwJysc8AY5RB9jB3/Pq8spipOZ
OML0DG9bklzhbYl/jK907ZMhpwYr8qXysh8nZBgnz6r+Lge7aIl3Y/RGLYNCwDoN
vyxy40EIN41zyN0nB06fP1tmJsPTHs7FCtuqXgKjFATz7AOHEnjSPoFx5DcReHEB
pZXbwDV8G/WUfgQA4opjbZ7SrbtHg07E8GZMtaiRjpME5ntsStSRbNVHYiPbPSjY
l3lYZ0mXVZqxRaWkfOwMp0t0xI4EuiUeHjRBvk6mEi1soAEwHfY1Qg2X2jvU+cAy
ZuVNo05CnxQyB5d7ylTbXrdqBu7/jrtyd9iZhNqS/Q2xG8UDLeDT4dXW8rU=
=63km
-----END PGP PUBLIC KEY BLOCK-----
```

And here is your private key, passphrase is `password`. Super secure :)

*Please note, do not use this private key anywhere*

```
-----BEGIN PGP PRIVATE KEY BLOCK-----
Version: Keybase OpenPGP v1.0.0
Comment: https://keybase.io/crypto

xcFFBFrGUr0BBADko60yTU5yXf3oPXVk2NzJaP9GUv7J4mpkAnhrcKlRg/C0WkJS
un+szDe9YXLbQXiW2Xdx1DbRQK1NLQfJZMiiUEmoWvrllmMqn2bBf9xmmeiOFBU9
M8PyhDxL5d3T32ph9+BItyEL/jk4XxSRw7JYT/8MrAmgIm9dtUSRN905mQARAQAB
/gkDCA5X4Xgs1thBYB28qjkOkGnB1PajwpVbckK2nwVhVmmxqZnGxt6cdrkbjujm
Pel4x8ejsU98BGRy+A21Mi4UfDlIs7JvfkzFABadZxE3E6QI02Ava4RXRgE8rQkJ
6oCUlAlSSP7L0aMI2Q8cVBYlR4Ys5RrdpTkx42kEwFhiO/T5TFCS3s0qrCjt9tCh
Qvp+d+crsBwKSlFZg4wJqbBDR4I7M7tKPcXI0kFynfjsKUVSvq43ZD2LtZbHJfLK
5TdJV3OVvleMPPhGtQRVAEofEFaCIszir1PyLRgqd7Urcj6alIgce2HZH2ea3AYY
ymNINV/aaKi1J+I7vLYojEMECjg6mHO5kgTXc1anNID3mwaY2OwcAq1o918gvgha
0/jDabQuRB60yzxGclnjEoLCu6kDs5q4jKo8Vo5Glz2rWVeYxhMQW4flUFbgLdlN
z/Imi4S5w1S+zqZyCVATY1LKWcT5u3vHXIApSPSyDg/sevDsREwX9c0iR2xhZGl1
cyBIaXJlZSA8Y2FyZWVyc0BnbGFkaXVzLmlvPsKtBBMBCgAXBQJaxlK9AhsvAwsJ
BwMVCggCHgECF4AACgkQOJkS2avka0B6VQP9H2d03SZicyY+7iblBQENgd62LmB/
q8oNC1VL202zvFoMVbsbU46w1S9MQdjNc1VYIfIPSV+oyi6Ff/IOvQW96Zh1GPmn
IwN5+MIcfPWwWy/Pl3NMav7SnJ8oVVooHIoKz4gStMH0dyCZQi5kiIoQnDSQ09GC
qi6Nv+D9lv0Ab/HHwUYEWsZSvQEEAMAU50K0XKJWqhVQlem6oCodfBzau/0lX2T2
BZlNrJcDr00NNPMjxBNKShEmP9a86FYHvAHRnAZsYqJT9rx4tEDNi8fEZwV2OlDe
nsiQ2dpIICa7tpks2o1PMxy8bpzAiJeO42p9+BqgzRFGEQWT+PKEd/61pm9kE31A
VOL/x/DBABEBAAH+CQMI9GtTF0a5EXtgB8DPQoDl+yWgY7QfzYKCSSAigi/Y8FJU
paVQigdchLEgo6hrQqUCvtSv6vF5RxVek2bTimyy9SVRC2ovrIjaIDKErRbghmlf
Qi1lea7GidvX6WC2Cqc+tyz9g7bTlI9tGS5Y4+vTjVGWV6eCXOS1U0jy+OvRIa9q
ftyuASe9sHE4WN7bI+Amp7JGPRirVNCKPsFInh/q64KNiKUSx8r+0tmrtTPhVvVt
OAI7n6rQzAoxQtw0lG+ZW0D7S+KePihAxi0MClbWoAoDDRooasJtRFkME3izG8h3
AUw9lxRCjzyGr9xdJzhPVxMpPFwMKIfj/EL1esMdw54+yH8Sl1W3iByVuTv7Hxbl
eCHq6Q/KvDEQYzJsuD4U6zGzQlE8Co+dnoROKOKamuT+v7vn/jnZ0CDU7Wa/64Jl
31I8MXCaH/S79z3xPM300Y+CbBsbBwrfbIRf2PC2oJeJzccNPJjS2TNRphRpaKVG
ORy2osLAgwQYAQoADwUCWsZSvQUJDwmcAAIbLgCoCRA4mRLZq+RrQJ0gBBkBCgAG
BQJaxlK9AAoJEB7UedMAB3/4HycEALsMFZntQRiqzQNy1TIIN/KdxkndXYQC6Dc7
u0EJgwzz81jlmwEKpHpluTz58p65hRfu465j2HAzGjPQP8Mcosu0tKCAQLYDwzX9
C4BBc94psjTyEi8da8lubgBdJjyhv4KMHG1zct/GazAahw3ek3spglOIeUiDOZN1
APa+eplEwd8EAJMZNbam1cUx5i9+ayarjYH1xtGFMQz7/S6icIK8MLPw4jDgd3oQ
XwYVFAc5t6yKbtd5SFk8xgrbx6nkZ/xCfCD3gl2tjFpqk742B2G31aF4A++UFr/K
6aAv0nObWuraIcpnkla0O8kU+dB/dDvln4JdtKsc1wPgRMrqyZWWZZ0mx8FGBFrG
Ur0BBAC15JKl7Sc0O9WwcRe1tLe8sRul6O5pyGt0phSxZnWH4iTCbSxjNvTPrPCx
Wr4a2yAajzxUojkvk9AfTiJ71Zr8WfCSHvYnBm5V3VVDnqh3Rt5MnFk0S2G2CBgG
78xXnQ4BfdXIJykJFEcWAxq9N/rxQDHfLsO91ejq0suY8E6OAwARAQAB/gkDCAg2
+IHs3CehYKW2vm42Ln7m20Cd9xpxFiROAEFmRwlxqFQHgmnEFh1NUpGWMBMf6uLU
qTiRVvV7vQ+3sA+IsnTbv/p+CScFCEZeMY8BneocVx3baeSC3CZ5Z0dzxHDkDri1
y90fDNcjmqy1i82EBvhaOPC5dOzNkJmWMzma0gk+OKbhZVswRHdl3lnNltxJEqcn
QzFDO/77/0mesmrGstFZoJMaBD1m0dzFqVz/FyEZYsB8LMiUUk+StlP4OP1SETVp
3qgpBQVSEAt9GF4HbOFtT7NZpzjqjLAq1dR+pME0RnsT8DZvkV1s9GdCTJWMfiVI
BkLGR8zFqgCuDJYS7FvyrrVRY4DopJMyPfzQdKFrP3ENVpfn7y2Xt1zxQ0OkX6FH
8IkSIlDJgA94JmFKoCW1TcBrWjQtA97A9UZMoXTPoDft6Ax1RP/5jZ7eyaGusIai
mGQy6wwhLYOCizWUTYzmJG9yxeVVy68AGkweUw71deCYJTDCwIMEGAEKAA8FAlrG
Ur0FCQ8JnAACGy4AqAkQOJkS2avka0CdIAQZAQoABgUCWsZSvQAKCRDf4cLmfBev
NnbNA/9AmEET9/AnKxzwBjlEH2MHf8+ryymKk5k4wvQMb1uSXOFtiX+Mr3TtkyGn
BivypfKyHydkGCfPqv4uB7toiXdj9EYtg0LAOg2/LHLjQQg3jXPI3ScHTp8/W2Ym
w9MezsUK26peAqMUBPPsA4cSeNI+gXHkNxF4cQGlldvANXwb9ZR+BADiimNtntKt
u0eDTsTwZky1qJGOkwTme2xK1JFs1UdiI9s9KNiXeVhnSZdVmrFFpaR87AynS3TE
jgS6JR4eNEG+TqYSLWygATAd9jVCDZfaO9T5wDJm5U2jTkKfFDIHl3vKVNtet2oG
7v+Ou3J32JmE2pL9DbEbxQMt4NPh1dbytQ==
=4GZS
-----END PGP PRIVATE KEY BLOCK-----
```

*Please note, do not use this private key anywhere*
