
// #----PARA DATASETS MAIS SIMPLES DE CONSULTA sql SimplesconsultaSentencaSQL #
// FUNÇÃO PARA GUARDAR OS CAMPOS QUE SERÃO CHAMADOS
  function campos(){
    // os 
    var campo = ["IDMOV","NOME","CODCFO","IDENTIFICACAO","NUMERONFSE","HISTORICO","PROTOCOLO","DATAAUTORIZACAO","EMAIL","CHAVE","DT"]; 
    return campo;
}

function defineStructure() {
	var COLUNAS = campos();
    for (var i=0; i < COLUNAS.length; i++ ) {
		addColumn(COLUNAS[i]);
	}
	setKey([COLUNAS[0]]);
	//addIndex([COLUNAS[1]]);
    }

function onSync(lastSyncDate) {
  var dataset = DatasetBuilder.newDataset();
	var COLUNAS = campos();
	for (var i=0; i < COLUNAS.length; i++ ) {
		dataset.addColumn(COLUNAS[i]);
	}
	DATASET QUE GUARDA AS CREDENCIAIS DO ACESSO RM: O USUARIO, SENHA, TOKEN, COLIGADA
	var ds_chave_rm = DatasetFactory.getDataset("ds_chave_rm", null, null, null);
  var chave = ds_chave_rm.getValue(0, "CHAVE");
  var codColigada	=ds_chave_rm.getValue(0, "CODCOLIGADA");
	var codConsulta		= "sql_ma_pesq_nfe"; // CONSULTA SQL CRIADA NO CORPORERM
	var codSistema		= "T"; // MODULO EM QUE A CONSULTA FOI ARMAZENADA
	var filter 			= ""; 
	var schema			= false;
	
		//Instanciando o servico e utilizando os metodos por autenticacao basica.
	var serviceName 	= "wsECM";						
	var servicePackage	= "org.tempuri.WsECM";
	var servico = ServiceManager.getService(serviceName);
	var serviceHelper = servico.getBean();
    var instancia = servico.instantiate(servicePackage);
    var ws = instancia.getWsECMSoap();
	var result = ws.consultaSentencaSQL(codColigada, codConsulta, codSistema, filter, schema, chave);
	var jsonObj = getTagsByName(result, 'Row');
		if(jsonObj.length > 0){
			for(var i=0;i<jsonObj.length;i++){
				var row = [];
				for(var j=0;j<COLUNAS.length;j++){
					var field = COLUNAS[j].toUpperCase(); 
					var tags = getTagsByName(jsonObj[i],field); 
					var regex = new RegExp('(<'+field+'>|<\/'+field+'>)','g');
					row.push(tags[0].replace(regex,''));
				}
				dataset.addOrUpdateRow(row);
			}
		}
	    
		return dataset;	
	
	
}

function getTagsByName(stringXML, tagName){
	var linarize = stringXML.replace("\n","").replace("\r","");
	var regex = new RegExp('<'+tagName+'>(.*?)<\/'+tagName+'>','g');
	var tags = linarize.match(regex);
	//log.info("#### tags: " + tags);
	if(tags == null){
		log.warn('@getTagsByName : Tag '+tagName+' nao foi encontrada no retorno da consulta.');
		return [''];
	}
	else return tags;
}

#---------------#
