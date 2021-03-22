### Documentação técnica sobre os passos da solução:

* Criado uma instância EC2 para o ambiente StandAlone com o Splunk na última versão, liberado a porta 8000 para acesso ao Console Web;
* Criado um usuário específico da Real Protect para administração do App;
* Feito o upload do arquivo de log do ecommerce e criado o app, index, sourcetype e 05 arquivos de lookup para melhor entendimento dos códigos dos logs;
* A dashboard foi criada estruturando o XML em BaseSearch's;

Link de Acesso:
* https://52.87.173.142:8000 ou https://ec2-52-87-173-142.compute-1.amazonaws.com:8000
* Usuário e Senha: realprotect
* Index: realprotect
* Sourcetype: ecommerce_app

Para a correta indexação dos logs no Splunk não foi possível utilizar o sourcetype default, dessa forma foi necessário ajustes para a indexação correta:

* Definido o formato do TimeStamp `(%Y/%m/%d  %H.%.M:%.S.%3N)`;
* Definido o o prefixo do timestamp, no caso o valor de _time;
* Também foi necessário alterar o formato de indexação do Valor e Frete que estavam com `,` para separação de moeda, fiz a conversão com `.`;
* Após esse ajuste antes da indexação, facilitou para que pudesse ser feito a soma e média dos valores;

Um detalhe importante, houve um problema identificado ao utilizar o iplocation, nem todos os IP's trouxeram as informações de Region e City, cerca de 02 mil resultados estavam em branco.
Foi necessário efetuar a seguinte correção:

* Dentro do path `$SPLUNK_HOME/share/` foi substítuido o arquivo `GeoLite2-City.mmdb` por um novo de outro site `https://db-ip.com/`
* Documentação: `https://docs.splunk.com/Documentation/Splunk/8.1.2/SearchReference/Iplocation`
* Após a importação e restart foi possível a utilização do iplocation com todos os resultados possíveis de forma assertiva, onde 100% dos IP's trouxeram resultados;




