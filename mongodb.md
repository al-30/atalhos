# Atalhos para mongodb

## Buscar por valores em intervalos

```
{
  Numero:{
    $in:['123','456','789']
  }
}
```

Buscar com and:

```mongodb
{
  "$and": [
    { "ProcessoDeSelecao.IdentificadorExterno": "2219" },
    { "InscricaoNumero": "0000000035" }
  ]
}
```

## Dicas

Para realizar ordenacao por um atributo onde ele possa conter valores 'null',
uma possivel solucao é adicionar um campo para busca. Dessa forma, um campo sera
adicionado na ordenacao no banco e removido na devolutiva.

No exemplo a seguir,em C#, quero ordernar pelo campo 'Colocacao', e quero que os
valores 'null' sejam os ultimos da lista

```c#
var pipeline = new[]
{
    new BsonDocument("$match", filtroBson),

    // cria campo auxiliar para tratar null
    new BsonDocument("$addFields", new BsonDocument("colocacaoSort",
        new BsonDocument("$cond", new BsonArray
        {
            new BsonDocument("$eq", new BsonArray { "$Colocacao", BsonNull.Value }),
            9999, // se null, empurra para o final
            "$Colocacao"
        })
    )),

    // ordena usando o campo auxiliar
    new BsonDocument("$sort", new BsonDocument
    {
        { "colocacaoSort", 1 }   ,      // garante 1,2,null
        { "TipoDePreSelecionado", 1 } // mantém ordenação do tipo
    }),

    // remove o campo auxiliar do resultado
    new BsonDocument("$project", new BsonDocument("colocacaoSort", 0)),

    new BsonDocument("$skip", skip),

    new BsonDocument("$limit", filtro.QuantidadePorPagina),
  };

 var options = new AggregateOptions
 {
     AllowDiskUse = true
 };

 var documentos = await Collection.Aggregate<PreSelecionadoDocument>(pipeline, options).ToListAsync();
```
