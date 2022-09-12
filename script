<?php
// conexão com banco
$hostname = "***.**.***.***"; $username = "*******"; $password = "********"; $dbname = "*******"; 
$usertable1 = "TableC100s"; $usertable2 = "TableC170s"; $usertable3 = "TableC190s";
$conexao = mysqli_connect($hostname, $username, $password);
mysqli_select_db($conexao ,$dbname);

$result = mysqli_query($conexao, "select * from $usertable3 order by id"); // select da tabela
$rows_da_tabela = mysqli_fetch_all($result);

$compras_internas = 0;
$compras_gerais = 0;
$contador = count($rows_da_tabela);

for ($i = 0; $i < $contador; $i++){ // buscando dados do select feito no $result
    $array_total = $rows_da_tabela[$i];
    if ($array_total[5] >= 5000){

        if ($array_total[5] <= 5999){

            $array_total[7] = str_replace([','], '.', $array_total[7]);
            $compras_gerais += $array_total[7];
            $compras_internas += $array_total[7];
            
        }        
    }else {
        $array_total[7] = str_replace([','], '.', $array_total[7]);
        $compras_gerais += $array_total[7];
    }
}
$valor_de_compras_internas = str_replace([','], '.', $compras_internas);
$valor_de_compras_gerais = str_replace([','], '.', $compras_gerais);

$meta = ($valor_de_compras_internas/$valor_de_compras_gerais) * 100;
$numero_final = number_format($meta, 2, '.');

$dbname = "*******"; 
$conexao = mysqli_connect($hostname, $username, $password);
mysqli_select_db($conexao ,$dbname);

$insert = "INSERT INTO `metas_realizadas_projeto` (`idmetas_realizadas_projeto`, `ano`, `ano_data`, `valor`, `perc_cumprimento_meta`, `perc_penalidade`, `projetos_idProjetos`, `tab_metas_projeto_idtab_metas_projeto`) VALUES (default, '2022', '2022', $valor_de_compras_internas, $numero_final, '1.00', $array_total[1], '4')";
mysqli_query($conexao, $insert);
echo "metas do projeto $array_total[1] inserida na tabela metas_realizadas_projeto.";
?>
