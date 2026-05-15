#Atividade Prática: Configuração Avançada de Servidor de Arquivos e Controle de Acesso no Debian CLI
---
# 🖧 Configuração e Testes do Servidor Samba. Livia de Melo Pondian

Este documento apresenta o processo completo de instalação, configuração e validação de um servidor Samba em ambiente Linux 🐧. O objetivo foi criar um sistema de compartilhamento de arquivos em rede com diferentes níveis de acesso para usuários específicos.

---

# 📡 Teste de Comunicação entre as Máquinas

Antes de iniciar a configuração do servidor Samba, foi realizado um teste de conectividade entre as máquinas da rede utilizando o comando:

```bash
ping <IP_DA_MÁQUINA>
```

Esse procedimento é fundamental para garantir que cliente e servidor conseguem se comunicar corretamente através da rede local 🌐.

✅ O teste confirmou que os pacotes estavam sendo enviados e recebidos sem perda de conexão, indicando que a comunicação entre os dispositivos estava funcionando corretamente.

![Ping entre máquinas](https://github.com/user-attachments/assets/853e97af-f1ae-4199-8df1-b9fc79373355)

---

# 👤 Criação dos Usuários do Sistema

Após validar a conectividade da rede, foram criados os usuários que seriam utilizados no ambiente Samba.

Os usuários possuem funções diferentes dentro do sistema, permitindo a aplicação de permissões específicas 🔐.

Exemplo de comando utilizado:

```bash
adduser nome_usuario
```

📌 Essa etapa é importante porque o Samba utiliza usuários do próprio sistema Linux para autenticação e controle de acesso aos compartilhamentos.

![Criando usuários](https://github.com/user-attachments/assets/c7e3dc2f-487b-4ae8-9625-e27376000193)

---

# 🔄 Atualização do Sistema Operacional

Antes da instalação dos serviços, foi realizada a atualização dos pacotes do sistema operacional utilizando os comandos:

```bash
apt update
apt upgrade
```

✅ Esse processo garante:

- 📦 Pacotes mais recentes;
- 🔒 Correções de segurança;
- ⚡ Melhor estabilidade do sistema;
- 🛠️ Compatibilidade com os serviços instalados posteriormente.

A atualização do sistema é uma prática essencial em ambientes Linux para evitar problemas durante instalações e configurações futuras.

![Update do sistema](https://github.com/user-attachments/assets/10f2f13c-14b3-48d6-8443-a5d926b6a162)

---

# 📦 Instalação do Samba

Com o sistema atualizado, foi iniciada a instalação do Samba utilizando o gerenciador de pacotes do Linux.

Comando utilizado:

```bash
apt install samba
```

🖥️ O Samba é responsável por permitir o compartilhamento de arquivos e diretórios entre computadores Linux e Windows através do protocolo SMB/CIFS.

Após a instalação, o servidor já passou a possuir suporte ao compartilhamento em rede.

![Instalando Samba](https://github.com/user-attachments/assets/31f5d65a-f570-46da-813f-2250c9ad5ee0)

---

# 🚀 Inicialização do Serviço Samba

Após a instalação do Samba, o serviço foi iniciado para disponibilizar os compartilhamentos na rede.

Exemplo de comando utilizado:

```bash
systemctl start smbd
```

Também foi possível habilitar a inicialização automática do serviço durante o boot do sistema:

```bash
systemctl enable smbd
```

✅ Com isso, o servidor Samba ficou ativo e pronto para aceitar conexões dos clientes da rede.

![Iniciando Samba](https://github.com/user-attachments/assets/413ea535-e8d0-43a8-b49f-f6a7895446d3)

---

# 🔐 Definição de Senhas dos Usuários Samba

Após criar os usuários do sistema, foi necessário cadastrar suas senhas no Samba utilizando:

```bash
smbpasswd -a nome_usuario
```

📌 O Samba mantém seu próprio sistema de autenticação, por isso as senhas precisam ser registradas separadamente.

Durante essa etapa:

- 🔑 As credenciais dos usuários foram configuradas;
- 👥 Os acessos individuais foram habilitados;
- 🔒 O sistema passou a exigir autenticação para acessar os compartilhamentos.

![Senha usuários](https://github.com/user-attachments/assets/99b37546-fc6a-43c7-b125-39832511e812)

---

# 🧾 Verificação da Versão do Samba

Para confirmar que o Samba foi instalado corretamente, foi executado o comando:

```bash
samba --version
```

✅ O sistema exibiu a versão instalada do serviço, comprovando que a instalação ocorreu sem erros.

Essa verificação também ajuda na identificação de compatibilidade e suporte das funcionalidades disponíveis.

![Versão Samba](https://github.com/user-attachments/assets/dc5ad59f-be67-488a-a149-bf424c51d789)

---

# ⚙️ Configuração do Arquivo `smb.conf`

A configuração principal do servidor Samba foi realizada através do arquivo:

```bash
/etc/samba/smb.conf
```

Nesse arquivo foram definidas:

- 📂 Pastas compartilhadas;
- 👥 Usuários autorizados;
- 🔒 Permissões de leitura e escrita;
- 🌐 Nome do compartilhamento;
- 🛡️ Restrições de acesso.

Cada usuário recebeu permissões específicas conforme sua função no sistema.

📌 Essa etapa foi essencial para garantir segurança e organização no ambiente de compartilhamento de arquivos.

![Configuração smb.conf](https://github.com/user-attachments/assets/4dd417bc-f14e-41c6-a1b8-f375fc2912c3)

---

# 📥 Instalação do `cifs-utils`

Na máquina cliente Linux, foi instalado o pacote:

```bash
cifs-utils
```

Esse pacote permite montar compartilhamentos Samba utilizando o protocolo CIFS/SMB.

Exemplo de instalação:

```bash
apt install cifs-utils
```

✅ Com ele, tornou-se possível conectar o cliente Linux ao servidor Samba e acessar os diretórios compartilhados como se fossem pastas locais 📂.

Essa ferramenta é essencial para realizar montagens manuais ou automáticas utilizando o arquivo `/etc/fstab`.

![Instalando cifs-utils](https://github.com/user-attachments/assets/ee22561f-e5c6-45ba-87a5-e1161ea5f1f3)

---

# 🖥️🔐 4. Validação de Acesso — Perfil Administrador (`admin_ti`)

Para realizar os testes práticos do ambiente Samba, a máquina cliente utilizou o pacote `cifs-utils` para efetuar a montagem do compartilhamento remoto. O acesso foi realizado através do comando `mount -t cifs`, utilizando as credenciais do usuário administrador `admin_ti`.

## ✅ Resultado Obtido

O acesso ao diretório compartilhado foi realizado com sucesso 🎉.  
Após a conexão, executamos um teste de escrita criando o arquivo `relatorio.txt` com o comando:

```bash
touch relatorio.txt
```

O servidor autorizou a operação sem apresentar erros, comprovando que o perfil administrador possui permissões completas de leitura ✍️ e escrita 📂 no compartilhamento.

📌 Isso confirma que as permissões configuradas para o usuário administrador estão funcionando corretamente.

![Teste Admin](https://github.com/user-attachments/assets/062baadc-b8e2-4de8-b92b-d3c578ca4fb2)

---

# 👨‍💻🔎 5. Validação de Acesso — Perfil Suporte (`suporte_ti`)

Na segunda etapa do teste, o compartilhamento foi desmontado 🔄 e um novo acesso foi realizado utilizando o usuário `suporte_ti`.

O principal objetivo desta validação era verificar se as restrições de escrita configuradas no Samba estavam realmente sendo aplicadas.

## ✅ Resultado Obtido

O usuário conseguiu:

- 📖 Visualizar arquivos existentes;
- 📂 Listar o conteúdo da pasta compartilhada;
- 👀 Ler o arquivo criado anteriormente pelo administrador.

Entretanto, ao tentar realizar operações de escrita, como:

```bash
touch teste.txt
```

ou

```bash
mkdir nova_pasta
```

o sistema retornou o erro:

```bash
Permission denied
```

🚫 Isso demonstra que o usuário possui apenas permissões de leitura, sem autorização para modificar ou criar arquivos no servidor.

📌 O teste comprova que as permissões granulares configuradas no Samba estão operando corretamente e garantindo a segurança do ambiente.

![Teste Suporte](https://github.com/user-attachments/assets/63bcecef-025b-467a-a263-2f102479c09c)

---

# 🔄💾 6. Persistência de Dados e Automontagem (`/etc/fstab`) DESAFIO FINAL👿

O mapeamento realizado manualmente com o comando `mount` funciona apenas temporariamente ⏳. Após reiniciar o sistema, a conexão é perdida automaticamente.

Para resolver esse problema e automatizar o processo 🚀, configuramos o arquivo:

```bash
/etc/fstab
```

## ⚙️ Objetivo da Configuração

A configuração no `fstab` permite que o sistema operacional monte automaticamente o compartilhamento Samba durante a inicialização do Linux 🐧.

Na instrução adicionada foram definidos:

- 🔐 Credenciais do usuário administrador;
- 🌐 Tipo de sistema de arquivos `cifs`;
- 📝 Codificação `utf8`, evitando problemas com acentuação;
- 🔄 Montagem automática no boot.

Com isso, o compartilhamento fica disponível automaticamente para o usuário, sem necessidade de executar comandos manuais após cada reinicialização ✅.

![Configuração fstab](https://github.com/user-attachments/assets/c694ed6c-2b17-4b82-a2f6-6e12d8cfcf33)

---
