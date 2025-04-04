<h1 style="font-weight: bold;">AWS S3 static website 💻</h1>

<h3>Criando e configurando um bucket amazon s3</h3>

- É importante que o nome do buckt seja único em um espaço global.
- Também é importante que a localização do bucket seja escolhida visando um local próximo, pois isso ajuda a reduzir a latência.
- Devemos habilitar as ACLs. Elas são uma maneira de configurar as permissões dentro de um bucket, mas também é possível configurá-las por meio de bucket-policies como faremos mais adiante.

<h3>Fazendo o upload de arquivos para a nuvem</h3>

- Aqui é necessário fazer o upload do arquivo index.html e da pasta com as imagens e arquivos de estilização. Eles subirão como objetos do bucket.

<h3>Configurando o website</h2>

- Nessa etapa, o website se tornará disponível para o mundo.
- Para habilitar a hospedagem do site com o bucket é preciso ir até "Propriedades" e indicar o arquivo index.html como o documento de índice.
- Assim que visitarmos a URL no nosso endpoint do bucket, iremos encontrar "403 Forbidden error!". Isso acontece porque apesar de nossos objetos no bucket serem públicos, os arquivos dentro deles permanecem completamente privados. Para isso precisamos ajustar suas configurações de acesso separadamente.
  

<h3>Tornando os objetos do s3 públicos</h3>

- Para resolver o erro 403, podemos atualizar as configurações de acesso. Usando ACLs nós faremos os nossos arquivos do bucket se tornarem públicos.


<h3>Usando bucket policies</h3>

- Usaremos buckets policies para controlar o acesso aos arquivos dentro do bucket. Assim poderemos impedir que pessoas deletem objetos dentro do bucket.
- Vamos usar a seguinte política:

```bash
{
    "Version": "2012-10-17",
    "Id": "MyBucketPolicy",
    "Statement": [
        {
            "Sid": "BucketPutDelete",
            "Effect": "Deny",
            "Principal": "*",
            "Action": "s3:DeleteObject",
            "Resource": "arn:aws:s3:::<bucket-name>/<object-name>”
        }
    ]
}
```
- Bucket policies são regras que determinam quem está autorizado ou não a fazer alguma coisa. O benefício de usar essas políticas está em ter um controle ainda maior de todas as ações que as pessoas estão ou não autorizadas a fazer. Enquanto as ACLs controlam somente o acesso a objetos individuais.
- O nosso bucket proibe todos de deletarem nossos objetos.

<h4>Finalizando</h4>

- Apóa essas configurações pode ser acessada por qualquer pessoa e o website estará visível.
- Nesse projeto foram usados os conceitos de políticas do bucket s3, index.html e sua URL do endpoint do bucket e ACLs e como elas controlam o acesso aos buckets.
