// referente a tag container
const container = document.querySelector(".container");
// referente ao button
const novo = document.querySelector("#novo");
// referente ao primeiro form
const formNovo = document.querySelector("#formNovo");
// referente ao segundo form
const formDetalhes = document.querySelector("#formDetalhes");

var cards = [
    {
        Nome_produto: "Coca Cola",
        Preco: "R$ 5,00"
    },
    {
        Nome_produto: "Guarana",
        Preco: "R$4,50"
    },
];

criarCards()


formNovo.addEventListener("submit", e => {
    e.preventDefault();
    cards.push({
        Nome_produto: formNovo.Nome_produto.value,
        Preco: formNovo.Preco.value
    });
    formNovo.Nome_produto.value = '';
    formNovo.Preco.value = '';
    modalNovo.classList.add("oculto");
    criarCards()
    toast(`Card adicionado com sucesso!`);

})

function criarCards() {
    container.innerHTML = '';
    cards.forEach((card, i) => {
        container.innerHTML += `
        <div class="card">
            <h2>${card.Nome_produto}</h2>
            <p>${card.Preco}</p>
            <button onclick='excluir(${i})'>Excluir</button>
            <button onclick='detalhes(${i})'>Detalhes</button>
        </div>
        `;
    });
}

function detalhes(indice) {
    document.querySelector("#modalDetalhes").classList.remove("oculto");
    formDetalhes.indice.value = indice;
    formDetalhes.Nome_produto.value = cards[indice].Nome_produto;
    formDetalhes.Preco.value = cards[indice].Preco;
}

formDetalhes.addEventListener("submit", e => {
    e.preventDefault();
    cards[formDetalhes.indice.value] = {
        Nome_produto: formDetalhes.Nome_produto.value,
        Preco: formDetalhes.Preco.value
    }
    modalDetalhes.classList.add("oculto");
    criarCards();
    toast(`Card atualizado com sucesso!`);
});


// CRUD PARA EXCLUIR
function excluir(indice) {
    if (confirm("Deseja realmente exclui o card " + indice + "?")) {
        cards.splice(indice, 1);
        criarCards();
        toast(`Card ${indice} excluído com sucesso!`);
    }
}

function toast(msg) {
    document.querySelector(".toast").innerHTML = msg;
    setTimeout(() => {
        document.querySelector("#toast").innerHTML = '';
    }, 3000);
}
