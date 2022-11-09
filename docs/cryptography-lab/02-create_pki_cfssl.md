# CFSSL 
CFSSL is CloudFlare's PKI/TLS swiss army knife. It is both a command line tool and an HTTP API server for signing, verifying, and bundling TLS certificates.

- Step 0 Install Golang
```
sudo apt install golang
```
- Step 1 Install CFSSL

Download the binary package for your system at https://github.com/cloudflare/cfssl/releases.Unzip the archive and run the cfssl binary.

- Step 2 Generate Root CA 

Create a config file for the root-ca ca.json and past the below
```
{
  "CN": "CyberbayKin Root CA",
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [
  {
    "C": "MM", 
    "L": "Yangon",
    "O": "CbyerbayKin",
    "OU": "CyberbayKin Root CA",
    "ST": "Myanmar"
  }
 ]
}

```
Enter the following command to generate "ca.pem" and "ca-key.pem"
```
cfssl gencert -initca ca.json | cfssljson -bare ca
```

- Step 3 Generate Intermediate CA

To generate the intermediate the following config file "intermediate-cs.json" is needed.
```
{
  "CN": "CyberbayKin Intermediate CA",
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [
    {
      "C":  "MM",
      "L":  "Yangon",
      "O":  "CyberbayKin",
      "OU": "CyberbayKin Intermediate CA",
      "ST": "Myanmar"
    }
  ],
  "ca": {
    "expiry": "42720h"
  }
}
```

Generate the intermediate key pairs with the following command
```
cfssl gencert -initca intermediate-ca.json | cfssljson -bare intermediate_ca
```

Then create the profile.json configuration file to sign
```
{
  "signing": {
    "default": {
      "expiry": "8760h"
    },
    "profiles": {
      "intermediate_ca": {
        "usages": [
            "signing",
            "digital signature",
            "key encipherment",
            "cert sign",
            "crl sign",
            "server auth",
            "client auth"
        ],
        "expiry": "8760h",
        "ca_constraint": {
            "is_ca": true,
            "max_path_len": 0, 
            "max_path_len_zero": true
        }
      },
     "client": {
        "usages": [
          "signing",
          "digital signature",
          "key encipherment", 
          "client auth"
        ],
        "expiry": "8760h"
      }
    }
  }
}
```

Sign the intermediate key pair with the root-ca by using the following command 
```
cfssl sign -ca ca.pem -ca-key ca-key.pem -config cfssl.json -profile intermediate_ca intermediate_ca.csr | cfssljson -bare intermediate_ca
```

!notes 
The second “sign” command uses the CA produced previously to sign the intermediate CA. It also uses the “cfssl.json” profile and specifies the “intermediate_ca” profile.

- Step 4 Generate Client Certificates 

Use the below config for the client1.json
```
{
  "CN": "client.cyberbaykin.com",
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [
  {
    "C": "MM"
    "L": "Yangon",
    "O": "Cyberbaykin",
    "OU": "Cyberbaykin Hosts",
    "ST": "Myanmar"
  }
  ],
  "hosts": [
    "client1.cyberbaykin.com",
    "localhost"
  ]
}
```

To generate the client certicate with the following command 

```
cfssl gencert -ca intermediate_ca.pem -ca-key intermediate_ca-key.pem -config cfssl.json -profile=client client1.json | cfssljson -bare host-1-client
```


- Extra How To Verify certificates with openssl 
https://www.misterpki.com/openssl-verify/


ref: https://rob-blackbourn.medium.com/how-to-use-cfssl-to-create-self-signed-certificates-d55f76ba5781
