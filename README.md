# LDAP
# # # COMO CRIAR UM GRUPO NO LDAP # # # 
# Criar um arquivo:
vim criaGrupo.ldif
# Inserir as informações no arquivo:
dn: ou=professores,dc=example,dc=com
objectClass: organizationalUnit
ou: professores
# Rodar o comando para add o grupo:
ldapadd -x -D "cn=admin,dc=example,dc=com" -w 1234 -H ldap:// -f createGroup.ldif
result: adding new entry "ou=professores,dc=example,dc=com"
PRONTO O GRUPO FOI CRIADO.
# Verificar: 
ldapsearch -x ou=professores -b dc=example,dc=com

# # # COMO CRIAR UM USUÁRIO NO LDAP # # # 
# Criar um arquivo:
vim createUser.ldif
# Inserir as informações no arquivo:
dn: uid=fulano,ou=professores,dc=example,dc=com
changetype: add
objectClass: inetOrgPerson
description: Fulano John Smith
 é um profesor da
 universidade.
cn: Fulano John Smith
sn: Fulano
uid: fulano
# Rodar o comando para add o usuário:
ldapadd -x -D "cn=admin,dc=example,dc=com" -w 1234 -H ldap:// -f createUser.ldif
# verificar:
 ldapsearch -x uid=fulano -b ou=professores,dc=example,dc=com

# # # COMO ADICIONAR UM ATRIBUTO A UM USUÁRIO # # # 
# Criar um arquivo: 
vim addAttribute.ldif
# Inserir as informações no arquivo (adicionar um email):
dn: uid=fulano,ou=professores,dc=example,dc=com
changetype: modify
add: mail
mail: fulano@example.com
# Rodar o commando:
ldapmodify -x -D "cn=admin,dc=example,dc=com" -w 1234 -H ldap:// -f addAttribute.ldif
# Verificar:
ldapsearch -x uid=fulano -b ou=professores,dc=example,dc=com

# # # COMO APAGAR UM ATRIBUTO DO USUARIO # # # 
# Criar um arquivo: 
vim deleteAttribute.ldif
# Inserir as informações no arquivo (apagar uma descrição):
dn: uid=fulano,ou=professores,dc=example,dc=com
changetype: modify
delete: description
Rodar o commando:
ldapmodify -x -D "cn=admin,dc=example,dc=com" -w 1234 -H ldap:// -f addAttribute.ldif
# Verificar:
ldapsearch -x uid=fulano -b ou=professores,dc=example,dc=com
ldapsearch -LLL -x -H ldap:// -t -b "dc=example,dc=com" "uid=fulano"

# adicionar a imagem no /tmp/

REFERÊNCIA
https://www.digitalocean.com/community/tutorials/how-to-use-ldif-files-to-make-changes-to-an-openldap-system
