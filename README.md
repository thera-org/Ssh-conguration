# Como fazer commit em redes privadas

## Passo 1: Gerar a chave SSH

1. **Abra o Git Bash.**
2. **Gere a chave SSH:**  
   No Git Bash, execute o comando abaixo para criar uma chave RSA sem senha, no formato PEM, e salvá-la em `~/.ssh/github_key`:
   ```bash
   ssh-keygen -m PEM -t rsa -P "" -f ~/.ssh/github_key
Esse comando gera dois arquivos:

-   `github_key` (chave privada)
-   `github_key.pub` (chave pública)

## Passo 2: Configurar o SSH

1.  **Acesse o diretório SSH:**
    
    `cd ~/.ssh` 
    
2.  **Crie o arquivo de configuração:**
    
    `touch config` 
    
3.  **Edite o arquivo de configuração:** Abra o arquivo com o editor Vim:
    
    `vim config` 
    
    Pressione a tecla `I` para entrar no modo de inserção e cole o conteúdo abaixo (use `Ctrl+Shift+Ins` para colar, se necessário):
    
    ```
    Host github.com
        HostName ssh.github.com
        User git
        PreferredAuthentications publickey
        IdentityFile ~/.ssh/github_key
        IdentitiesOnly yes
        Port 443
    ```
    
4.  **Salve e saia do Vim:**  
    Pressione `ESC` e digite `:wq` para salvar as alterações e fechar o editor.
## Passo 3: Adicionar a chave pública ao GitHub

1.  **Exiba sua chave pública:**
    `cat github_key.pub` 
2.  **Copie o conteúdo exibido.**
3.  **Adicione a chave no GitHub:**  
    No seu navegador, acesse sua conta do GitHub e vá para _Settings > SSH and GPG keys_. Clique em "New SSH key" e cole o conteúdo copiado.

## Passo 4: Testar a conexão SSH

1.  **Teste a autenticação:**
    `ssh -T git@github.com`   
2.  **Verifique a mensagem de sucesso:**  
    Se tudo estiver correto, você verá uma mensagem similar a:    
    `Hi [username]! You've successfully authenticated, but GitHub does not provide shell access.` 
    
    Essa mensagem confirma que sua configuração SSH foi realizada com sucesso.
