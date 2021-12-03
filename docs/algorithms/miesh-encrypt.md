# Create encrypt algorithm

## Requirements

* Identify the input data, the purpose and the output data.
* Review Ruby OpenSSL::Cipher documentation.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://ruby-doc.org/stdlib-2.4.0/libdoc/openssl/rdoc/OpenSSL/Cipher.html)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating the algorithm

* Goto [algorithms](https://cenit.io/algorithm) module.
* Select the action [add new](https://cenit.io/algorithm/new) to create the new algorithm.
* Complete the form fields with the information corresponding to the algorithm in question.

    >- **Namespace**: Miesh
    >- **Name**: encrypt
    >- **Parameters**: key, iv, data
    >- **Language**: Ruby
    >- **Code**: Code snippet written in the Ruby language to encrypt a data buffer.

    > **Note**: The algorithms that are not specific to some integration, it is recommended to define them under a common namespace for all integrations.

## Code snippet

```ruby
cipher = OpenSSL::Cipher.try(:new, 'AES-256-CBC')
cipher.encrypt # set cipher to be encryption mode
cipher.key = key
cipher.iv = iv

encrypted = ''
encrypted << cipher.update(data)
encrypted << cipher.final

Base64.encode64(encrypted).gsub(/\n/, '')
```

## Snapshots of the process

### Goto algorithm module

   ![](assets/snapshots/common-algs/snapshots-001.png)
    
### Add new algorithm

   ![](assets/snapshots/common-algs/snapshots-002.png)
   ![](assets/snapshots/miesh-encrypt-decrypt-algs/snapshots-003.png)
