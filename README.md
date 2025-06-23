const produtos = [
    { id: 1, nome: 'Bermuda Jeans Escura', preco: 59.99, imagem: '1000067117.jpg' },
    { id: 2, nome: 'Bermuda Jeans Lacoste', preco: 59.99, imagem: '1000067118.jpg' },
    { id: 3, nome: 'Bermuda Jeans John John', preco: 59.99, imagem: '1000067119.jpg' },
    { id: 4, nome: 'Bermuda Jeans Claro John John', preco: 59.99, imagem: '1000067120.jpg' },
    { id: 5, nome: 'Bermuda Jeans Clara', preco: 59.99, imagem: '1000067121.jpg' },
    { id: 6, nome: 'Bermuda Branca Rasgada Lacoste', preco: 59.99, imagem: '1000067124.jpg' },
];

const carrinho = [];
const produtosContainer = document.getElementById('produtos');
const listaCarrinho = document.getElementById('lista-carrinho');
const finalizarCompraBtn = document.getElementById('finalizar-compra');
const resumoPedido = document.getElementById('resumo-pedido');

function renderizarProdutos() {
    produtos.forEach(produto => {
        const card = document.createElement('div');
        card.className = 'produto-card';
        card.innerHTML = `
            <img src="${produto.imagem}" alt="${produto.nome}" />
            <h3>${produto.nome}</h3>
            <p>R$ ${produto.preco.toFixed(2)}</p>
            <button onclick="adicionarAoCarrinho(${produto.id})">Adicionar ao carrinho</button>
        `;
        produtosContainer.appendChild(card);
    });
}

function adicionarAoCarrinho(id) {
    const produto = produtos.find(p => p.id === id);
    carrinho.push(produto);
    atualizarCarrinho();
}

function atualizarCarrinho() {
    listaCarrinho.innerHTML = '';
    carrinho.forEach(item => {
        const li = document.createElement('li');
        li.textContent = `${item.nome} - R$ ${item.preco.toFixed(2)}`;
        listaCarrinho.appendChild(li);
    });
}

finalizarCompraBtn.addEventListener('click', () => {
    if (carrinho.length === 0) {
        alert('Seu carrinho está vazio!');
        return;
    }
    let total = carrinho.reduce((sum, item) => sum + item.preco, 0);
    resumoPedido.textContent = `Total: R$ ${total.toFixed(2)}`;
});

renderizarProdutos();
