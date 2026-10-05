# triggers
---
atividade1 

***TypeScript***
```typescript
class BancoDadosSimulado {
    produtos = [];
    historico = [];
    proximoIdProduto = 1;
    proximoIdHistorico = 1;
    dispararTrigger(itemAntigo, itemNovo) {
        let historicoNovo = {
            id: this.proximoIdHistorico,
            produto_id: itemNovo.id,
            quantidade_anterior: itemAntigo.quantidade,
            quantidade_nova: itemNovo.quantidade,
            data_alteracao: new Date()
        };
        this.historico.push(historicoNovo);
        this.proximoIdHistorico = this.proximoIdHistorico + 1;
    }
    inserir(nome, quantidade) {
        let prod = {
            id: this.proximoIdProduto,
            nome: nome,
            quantidade: quantidade
        };
        this.produtos.push(prod);
        this.proximoIdProduto = this.proximoIdProduto + 1;
    }
    atualizar(nome, novaQuantidade) {
        let posicao = -1;
        for (let i = 0; i < this.produtos.length; i++) {
            if (this.produtos[i].nome == nome) {
                posicao = i;
            }
        }
        if (posicao != -1) {
            let itemAntigo = {
                id: this.produtos[posicao].id,
                nome: this.produtos[posicao].nome,
                quantidade: this.produtos[posicao].quantidade
            };
            this.produtos[posicao].quantidade = novaQuantidade;
            let itemNovo = this.produtos[posicao];
            this.dispararTrigger(itemAntigo, itemNovo);
        }
    }
    mostrarTudo() {
        return this.historico;
    }
}
function rodar() {
    let bd = new BancoDadosSimulado();
    bd.inserir('Produto A', 100);
    bd.inserir('Produto B', 200);
    bd.atualizar('Produto A', 90);
    bd.atualizar('Produto A', 75);
    let final = bd.mostrarTudo();
    console.table(final);
}
rodar();

```
