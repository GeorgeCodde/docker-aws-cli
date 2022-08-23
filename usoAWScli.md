# Comadnos utilicados para docker con amazon aws cli y borrar vault's de S3 glacier

> Configurar las credenciales

```
docker run --rm -it -v awsCli:/root/.aws  amazon/aws-cli configure
```

- Listar los buckets de s3

```
docker run --rm -it -v awsCli:/root/.aws  amazon/aws-cli s3 ls
```

- Determinar que la configuración de las credenciales es visible

```
docker run --rm -it -v awsCli:/root/.aws amazon/aws-cli configure list
```

- Obtener información del vault

```
docker run --rm -it -v awsCli:/root/.aws amazon/aws-cli glacier describe-vault --vault-name BACASESORIA_0011328EE72A_1 --account-id 973770670162
```

- Iniciar un trabajo de recuperacion de inventario

```
docker run --rm -it -v awsCli:/root/.aws amazon/aws-cli glacier initiate-job --vault-name BACASESORIA_0011328EE72A_1 --account-id 973770670162 --job-parameters '{"Type": "inventory-retrieval"}'
```

- Para comprobar el estado del job de recuperacion de inventario

```
docker run --rm -it -v awsCli:/root/.aws amazon/aws-cli glacier describe-job --vault-name BACASESORIA_0011328EE72A_1 --account-id 973770670162 --job-id 3yyCYQlb6zhTQkFsTrgJEu3jCIR01j7ecn0eD6wQpc-WJQJvO8mpltbxKSAFvQfE13n-2p3x9AnYBHx1yLM8wieq2euy
```

- Descargar el resultado del inventario (Hasta que el trabajo termine, revisar con el comando anterior)

```
docker run --rm -it -v awsCli:/root/.aws amazon/aws-cli glacier get-job-output --vault-name BACASESORIA_0011328EE72A_1 --account-id 973770670162 --job-id 3yyCYQlb6zhTQkFsTrgJEu3jCIR01j7ecn0eD6wQpc-WJQJvO8mpltbxKSAFvQfE13n-2p3x9AnYBHx1yLM8wieq2euy output.json
```
