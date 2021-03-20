### Documentação técnica sobre os passos da solução:

* Criado uma instância EC2 para o ambiente StandAlone com o Splunk na última versão, liberado a porta 8000 para acesso ao Console;
* Criado um usuário específico da Real Protect para administração do App;
* Feito o upload do arquivo de log do ecommerce e criado um index, sourcetype e 05 arquivos de lookup para melhor entendimento dos códigos;

Para a correta indexação dos logs no Splunk não foi possível utilizar o sourcetype default, dessa forma foi necessário ajustes para a indexação correta:
1) Definido o formato do TimeStamp (%Y/%m/%d  %H.%.M:%.S.%3N);
2) Definido o o prefixo do timestamp, no caso o valor de _time;
3) Também foi necessário alterar o formato dos campos Valor e Frete que estavam com "," para separação de moeda, fiz a conversão com "."
4) Após esse ajuste antes da indexação, facilitou para que pudesse ser feito a soma e média dos valores dos produtos;

Um detalhe importante, houve um problema identificado ao utilizar o iplocation, nem todos os IP's trouxeram as informações de Region e City, cerca de 02 mil resultados estava em branco.
Foi necessário efetuar a seguinte correção:

01) Dentro do path `$SPLUNK_HOME/share/` foi substítuido o arquivo `GeoLite2-City.mmdb` por um novo de outro site `https://db-ip.com/`
02) Para esse caso segui as documentações da própria Splunk: https://docs.splunk.com/Documentation/Splunk/8.1.2/SearchReference/Iplocation


