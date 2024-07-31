# 🚀 Sejam todos bem-vindos ao meu repositório CadCommerce

## Índice
- [Conexão de Banco de Dados](#conex%C3%A3o-de-banco-de-dados)
- [Descrição](#descri%C3%A7%C3%A3o)
- [Introdução](#introdu%C3%A7%C3%A3o)
- [Funcionalidades](#funcionalidades)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Fontes Consultadas](#fontes-consultadas)
- [Autores](#autores)

# 💾 Conexão de Banco de Dados
<img src="img/tabela.png" width="40%">

# ✅ Descrição
Este código foi desenvolvido para demonstrar a configuração e utilização de uma conexão de banco de dados MySQL utilizando PHP. Ele faz parte do projeto CadCommerce.

# 📃 Introdução
Neste repositório, você encontrará exemplos de como configurar a conexão com o banco de dados, criar tabelas, e realizar operações CRUD (Create, Read, Update, Delete) usando PHP e MySQL.

## 🔧 Funcionalidades
- Configuração de conexão com banco de dados MySQL.
- Criação de tabelas no banco de dados.
- Inserção, leitura, atualização e exclusão de dados nas tabelas.

## 📁 Estrutura do Projeto
- `config.php`: Arquivo de configuração da conexão com o banco de dados.
- `categoria.php`: Gerenciamento de categorias.
- `marca.php`: Gerenciamento de marcas.
- `produto.php`: Gerenciamento de produtos.
- `pedido.php`: Gerenciamento de pedidos.
- `carrinho.php`: Gerenciamento do carrinho de compras.

## 📌 Tecnologias Utilizadas
- HTML5    
- CSS3   
- PHP 8.1   
- MySQL

# 📝 Métodos PHP Utilizados

## Configuração de Conexão
### `coneção.php`
```php
<?php
$servidor = "localhost";
$usuario = "root";
$senha = "";
$dbname = "cadcommerce";

$mysqli = new mysqli($servidor, $usuario, $senha, $dbname);

if($mysqli->connect_error) {
    die("Falha na conexão: " . $mysqli->connect_error);
}
?>
```
## Configuração de produto
### `produtos_3A.php`
```php
<?php
    // Inclui o arquivo de conexão com o banco de dados
    include_once('controller/conexao.php');
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de produtos</title>
    <!-- Link para o arquivo CSS -->
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <div class="center">
            <h1>Cadastro de produto</h1>
            <!-- Link para voltar à página inicial -->
            <a href="index.php" target="_self">Voltar</a>
        </div>
    </header>
    <section id="produtos">
        <!-- Formulário para cadastro de produtos -->
        <form action="insere-produto.php" method="post">
            Nome: <input type="text" name="nome"><br>
            Descrição: <input type="text" name="descricao"><br>
            Estoque: <input type="number" name="estoque"><br>
            Preço: <input type="number" name="preco" min="0.00" max="10000.00" step="0.01"><br>
            Categoria:
            <!-- Seleção de categoria -->
            <select name="seleciona_categoria" id="">
                <option value="">selecione</option>
                <?php
                    // Consulta todas as categorias do banco de dados
                    $resultado_categoria = "SELECT * FROM categoria";
                    $resultadocategoria = mysqli_query($mysqli, $resultado_categoria);
                    // Loop para preencher o dropdown com as categorias
                    while($row_categorias = mysqli_fetch_assoc($resultadocategoria)){ ?>
                    <option value="<?php echo $row_categorias['IDCATEGORIA'] ?>">
                    <?php echo $row_categorias['DESCRICAO'] ?></option>
                 <?php
                    }
                ?>
            </select>
            <br>
            Marca:
            <!-- Seleção de marca -->
            <select name="seleciona_marca" id="">
                <option value="">selecione</option>
                <?php
                    // Consulta todas as marcas do banco de dados
                    $resultado_marca = "SELECT * FROM marca";
                    $resultadomarca = mysqli_query($mysqli, $resultado_marca);
                    // Loop para preencher o dropdown com as marcas
                    while($row_marcas = mysqli_fetch_assoc($resultadomarca)){ ?>
                    <option value="<?php echo $row_marcas['IDMARCA'] ?>">
                    <?php echo $row_marcas['DESCRICAO'] ?></option>
                 <?php
                    }
                ?>
            </select>
            <br><br>
            <!-- Botão para submeter o formulário -->
            <input type="submit" value="Cadastrar">
        </form>
    </section>
</body>
</html>
```
## Configuração de marca
### `marca.php`
```php

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de marca</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <div>
            <h1>Cadastro de marca</h1>
            <a href="index.php" target="_self">Voltar</a>
        </div>
    </header>
    <section id="produtos">
        <form action="insere-marca.php" method="post">
            <label for="">Descrição: </label>
            <input type="text" name="descricao">
            <input type="submit" value="Cadastrar">
        </form>
    </section>
</body>
</html>
```
## Configuração de categoria
### `categoria.php`
```php

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de Categorias</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <div>
            <h1>Cadastro de Categoria</h1>
            <a href="index.php" target="_self">Voltar</a>
        </div>
    </header>
    <section id="produtos">
        <form action="insere-categoria.php" method="post">
            <label for="">Descrição: </label>
            <input type="text" name="descricao">
            <input type="submit" value="Cadastrar">
        </form>
    </section>
</body>
</html>
 
```
## inserindo categorias no banco
### `insere_produto.php`
```php
<?php
     include_once('controller/conexao.php');
     
     $categoria      = $_POST['seleciona_categoria'];
     $marca          = $_POST['seleciona_marca'];
     $nome_produto   = $_POST['nome'];    
     $descricao      = $_POST['descricao'];
     $estoque        = $_POST['estoque'];
     $preco          = $_POST['preco'];
    
     $grava_produto = "INSERT INTO produtos(`IDCATEGORIA`, `IDMARCA`, `NOME`, `DESCRICAO`, `ESTOQUE`, `PRECO`) VALUES (' $categoria ','$marca  ','$nome_produto','$descricao','$estoque','$preco')";

     $result_gravacao = mysqli_query($mysqli, $grava_produto);

     if(mysqli_affected_rows($mysqli) !=0){
        echo"
        <META HTTP-EQUIV=REFRESH CONTENT = '0,URL=produtos.php'>
        <script type=\"text/javascript\">
        alert('Produto cadastrado com sucesso');
        </script>
        ";
        
     }else{
        echo"
        <META HTTP-EQUIV=REFRESH CONTENT = '0,URL=produtos.php'>
        <script type=\"text/javascript\">
        alert('Produto não cadastrado');
        </script>
        ";
     }
?>
```
## inserindo marcas no banco
### `marcas.php`
```php
<?php
include('controller/conexao.php');

$descricao = $_POST['descricao'];

echo "<h3>Descrição: $descricao </h3></br>";

$cad_marca = "INSERT INTO marca(`DESCRICAO`) VALUES ('$descricao')";

if(mysqli_query($mysqli, $cad_marca)){
    echo "<h1>marca cadastrada com sucesso!</h1></br>";
}else{
    echo"Erro: ". $cad_marca. "</br>";
    mysqli_error($mysqli);

}mysqli_close($mysqli);
?>
```
## inserindo categorias no banco de dados
### `categoria.php`
```php
<?php
include('controller/conexao.php');

$descricao = $_POST['descricao'];

echo "<h3>Descrição: $descricao </h3></br>";

$cad_categoria = "INSERT INTO categoria(`DESCRICAO`) VALUES ('$descricao')";

if(mysqli_query($mysqli, $cad_categoria)){
    echo "<h1>categoria cadastrada com sucesso!</h1></br>";
}else{
    echo"Erro: ". $cad_categoria. "</br>";
    mysqli_error($mysqli);

}mysqli_close($mysqli);
?>

```
