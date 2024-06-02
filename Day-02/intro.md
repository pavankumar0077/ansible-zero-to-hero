## PASSWORD LESS AUTHENTICATION

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/9c58e42d-dc6b-475a-922e-725ded7d529f)

- It is not possible to login without using AUTHENTICATION.
- THEIR ARE 2 WAYS TO AUTHENTICATE
- 1. PASSWORD
- 2. SSH KEYS (PUBLIC KEY, PRIVATE KEY) - PUBLIC KEY IS SET UP IN TARGET VM, -- AND USING PRIVATE KEY WE CAN TALK TO THEM.

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/e344483d-8220-4f1f-913b-053348829667)

NOTE : WHEN WE TRY TO CONNECT TO THE VM, It will ask for SSH KEY PEM FILE OR PASSWORD.
--

- From Control node VM, if we are trying to access using SSH, TRUST CONTROL NODE VM, always ALLOW ACCESS FROM CONTROL NODE VM.
- Anytime if we get a request form VM - A, to VM-B do not ask for password. IN VM-B we have to say that always allow VM-A without a password. This machaism is called passwordless authentication.
- ONLY FOR THE 1ST TIME WE NEED TO PROVIDE THE ACCESS FROM VM-A TO VM-B USING PASSWORD OR PEM ( ONLY ONE TIME ACTION ONLY ONCE WE NEED TO DO THIS )

- WE CAN DO THIS IN 2 WAYS, USING PASSWORD OR SSH-KEY. BYDEFAULT EC2 INSTANCE WILL BLOCK THE PASSWORD AUTHENTICATION, WE NEED TO USE SSH KEY.

  
