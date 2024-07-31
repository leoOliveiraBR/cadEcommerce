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

###produtos3
```php
<?php
    include_once('controller/conexao.php');
    ?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de produtos</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <div class="center">
            <h1>Cadastro de produto</h1>
            <a href="index.php" target="_self">Voltar</a>
        </div>
    </header>
    <section id="produtos">
        <form action="insere-produto.php" method="post">
            Nome: <input type="text" name="nome"><br>
            Descrição: <input type="text" name="descricao"><br>
            Estoque: <input type="number" name="estoque"><br>
            Preço: <input type="number" name="preco" min="0.00" max="10000.00" step="0.01"><br>
            Categoria:
            <select name="seleciona_categoria" id="">
                <option value="">selecione</option>
                <?php
                    $resultado_categoria = "SELECT * FROM categoria";
                    $resultadocategoria = mysqli_query($mysqli, $resultado_categoria);
                    while($row_categorias = mysqli_fetch_assoc ($resultadocategoria)){ ?>
                    <option value="<?php echo $row_categorias['IDCATEGORIA'] ?>">
                    <?php echo $row_categorias['DESCRICAO'] ?></option>
                 <?php
                    }
                ?>
            </select>
            <br>
            Marca:
            <select name="seleciona_marca" id="">
                <option value="">selecione</option>
                <?php
                    $resultado_marca = "SELECT * FROM marca";
                    $resultadomarca = mysqli_query($mysqli, $resultado_marca);
                    while($row_marcas = mysqli_fetch_assoc($resultadomarca)){ ?>
                    <option value="<?php echo $row_marcas['IDMARCA'] ?>">
                    <?php echo $row_marcas['DESCRICAO'] ?></option>
                 <?php
                    }
                ?>
            </select>
            <br><br>
            <input type="submit" value="Cadastrar">
        </form>
    </section>
</body>

