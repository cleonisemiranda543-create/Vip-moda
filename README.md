<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Loja de Roupas - Samuel</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.6.0/css/all.min.css">

<style>
* { margin:0; padding:0; box-sizing:border-box; }
body { font-family: Arial, sans-serif; background:#fff; color:#111; line-height:1.6; overflow-x:hidden; }
html { scroll-behavior: smooth; }

/* HEADER */
header { background:#f5f5f5; padding:20px; text-align:center; border-bottom:1px solid #ddd; }
header h1 { font-size:28px; margin-bottom:5px; }
header p { color:#555; }

/* NAV */
nav { display:flex; justify-content:center; background:#fff; border-bottom:1px solid #ddd; flex-wrap:wrap; gap:20px; padding:12px 0; position:sticky; top:0; z-index:100; }
nav a { color:#111; text-decoration:none; font-weight:bold; display:flex; align-items:center; gap:6px; padding:6px 10px; border-radius:5px; transition:.3s; }
nav a:hover { background:#f0f0f0; }

/* BANNER */
.banner { background:#e0f7fa; padding:60px 20px; text-align:center; }
.banner h2 { font-size:32px; margin-bottom:10px; color:#00796b; }
.banner p { font-size:18px; color:#004d40; }

/* PRODUTOS */
.produtos { display:grid; grid-template-columns:repeat(auto-fit,minmax(250px,1fr)); gap:20px; padding:30px 20px; }
.card { border:1px solid #ddd; border-radius:10px; overflow:hidden; box-shadow:0 2px 6px rgba(0,0,0,0.1); transition:.3s; background:#fff; display:flex; flex-direction:column; }
.card:hover { transform:translateY(-5px); box-shadow:0 5px 15px rgba(0,0,0,0.15); }
.card img { width:100%; height:300px; object-fit:cover; }
.card-content { padding:15px; flex:1; display:flex; flex-direction:column; justify-content:space-between; }
.card-content h3 { margin-bottom:10px; font-size:20px; }
.card-content .preco { font-weight:bold; margin-bottom:10px; display:flex; align-items:center; gap:5px; }
.card-content button { background:#00796b; color:#fff; border:none; padding:10px; border-radius:5px; cursor:pointer; font-size:16px; display:flex; align-items:center; justify-content:center; gap:6px; transition:.3s; }
.card-content button:hover { background:#004d40; }

/* SOBRE */
#sobre { background:#f9f9f9; padding:40px 20px; text-align:center; }
#sobre h2 { margin-bottom:15px; font-size:28px; }
#sobre p { max-width:700px; margin:0 auto; color:#555; font-size:18px; }

/* CARRINHO */
.carrinho { position:fixed; top:100px; right:20px; background:#fff; border:1px solid #ddd; border-radius:10px; width:300px; max-height:70vh; overflow-y:auto; box-shadow:0 5px 15px rgba(0,0,0,0.2); padding:15px; z-index:200; }
.carrinho h3 { margin-bottom:15px; font-size:20px; text-align:center; }
.carrinho-item { display:flex; justify-content:space-between; margin-bottom:10px; align-items:center; }
.carrinho-item button { background:red; color:#fff; border:none; border-radius:4px; cursor:pointer; padding:2px 6px; }
.carrinho-total { font-weight:bold; margin-top:10px; text-align:right; }

/* MODAL */
.modal { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.6); justify-content:center; align-items:center; z-index:300; }
.modal-content { background:#fff; padding:30px; border-radius:10px; max-width:400px; width:90%; text-align:center; animation:fadeIn .3s; }
.modal-content h3 { margin-bottom:15px; }
.modal-content img { max-width:200px; margin:15px 0; }
.modal-content input { width:80%; padding:10px; margin:5px 0; border-radius:5px; border:1px solid #ccc; font-size:16px; }
.modal-content input:focus { outline:none; border-color:#00796b; box-shadow:0 0 5px #00796b; }

/* BUTTONS */
.modal-content button { margin:10px; padding:10px 20px; border:none; border-radius:6px; cursor:pointer; font-size:16px; transition:.3s; }
#pix { background:#4caf50; color:#fff; }
#pix:hover { background:#388e3c; }
#cartao { background:#2196f3; color:#fff; }
#cartao:hover { background:#1565c0; }
#fecharModal { background:#f44336; color:#fff; }
#fecharModal:hover { background:#c62828; }
#confirm { background:#00796b; color:#fff; }
#confirm:hover { background:#004d40; }

/* CONFETE */
.confete { position:fixed; width:10px; height:10px; background:red; z-index:500; animation:confeteFall 3s linear forwards; }
@keyframes confeteFall { 0% { transform:translateY(0) rotate(0deg);} 100% { transform:translateY(100vh) rotate(360deg); opacity:0;} }

@keyframes fadeIn { from {opacity:0} to {opacity:1} }

/* FOOTER */
footer { text-align:center; padding:20px; background:#f5f5f5; border-top:1px solid #ddd; margin-top:30px; }

/* RESPONSIVIDADE */
@media(max-width:768px){ nav{flex-direction:column; gap:10px;} .card img{height:250px;} .carrinho{width:90%; top:80px; right:50%; transform:translateX(50%);} }
@media(max-width:480px){ header h1{font-size:24px;} .banner h2{font-size:26px;} .banner p{font-size:16px;} .card img{height:200px;} }
</style>
</head>
<body>

<header>
<h1><i class="fa-solid fa-shirt"></i> Loja de Roupas - Samuel</h1>
<p>As melhores roupas com os melhores preços!</p>
</header>

<nav>
  <a href="#produtos"><i class="fa-solid fa-box-open"></i> Produtos</a>
  <a href="#sobre"><i class="fa-solid fa-circle-info"></i> Sobre</a>
  <a href="#contato"><i class="fa-solid fa-envelope"></i> Contato</a>
  <a href="#" onclick="toggleCarrinho()"><i class="fa-solid fa-cart-shopping"></i> Carrinho (<span id="carrinho-count">0</span>)</a>
</nav>

<section class="banner">
<h2>Promoções de Roupas!</h2>
<p>Compre agora e garanta seu estilo com descontos incríveis.</p>
</section>

<section id="produtos" class="produtos">
<!-- PRODUTOS -->
<div class="card">
  <img src="https://images.unsplash.com/photo-1600185368191-5ce8c0b4a2a2?auto=format&fit=crop&w=400&q=80" alt="Camiseta Branca">
  <div class="card-content">
    <h3>Camiseta Branca</h3>
    <div class="preco"><i class="fa-solid fa-dollar-sign"></i> 49,90</div>
    <button onclick="adicionarCarrinho('Camiseta Branca',49.90)"><i class="fa-solid fa-cart-plus"></i> Adicionar</button>
  </div>
</div>
<div class="card">
  <img src="https://images.unsplash.com/photo-1600185367765-9d6d04cf0e2c?auto=format&fit=crop&w=400&q=80" alt="Calça Jeans">
  <div class="card-content">
    <h3>Calça Jeans</h3>
    <div class="preco"><i class="fa-solid fa-dollar-sign"></i> 129,90</div>
    <button onclick="adicionarCarrinho('Calça Jeans',129.90)"><i class="fa-solid fa-cart-plus"></i> Adicionar</button>
  </div>
</div>
<div class="card">
  <img src="https://images.unsplash.com/photo-1541099649105-f69ad21f3246?auto=format&fit=crop&w=400&q=80" alt="Jaqueta Preta">
  <div class="card-content">
    <h3>Jaqueta Preta</h3>
    <div class="preco"><i class="fa-solid fa-dollar-sign"></i> 199,90</div>
    <button onclick="adicionarCarrinho('Jaqueta Preta',199.90)"><i class="fa-solid fa-cart-plus"></i> Adicionar</button>
  </div>
</div>
<div class="card">
  <img src="https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?auto=format&fit=crop&w=400&q=80" alt="Vestido Floral">
  <div class="card-content">
    <h3>Vestido Floral</h3>
    <div class="preco"><i class="fa-solid fa-dollar-sign"></i> 149,90</div>
    <button onclick="adicionarCarrinho('Vestido Floral',149.90)"><i class="fa-solid fa-cart-plus"></i> Adicionar</button>
  </div>
</div>
</section>

<section id="sobre">
<h2>Sobre Nós</h2>
<p>A Loja de Roupas Samuel oferece moda de qualidade com preços acessíveis. Trabalhamos para que você tenha estilo e conforto em qualquer ocasião!</p>
</section>

<div class="carrinho" id="carrinho" style="display:none;">
<h3><i class="fa-solid fa-cart-shopping"></i> Seu Carrinho</h3>
<div id="itens-carrinho"></div>
<div class="carrinho-total">Total: R$ <span id="total">0.00</span></div>
<button onclick="abrirPagamento()" style="margin-top:10px; width:100%; background:#00796b; color:#fff; padding:10px; border:none; border-radius:5px;">
<i class="fa-solid fa-credit-card"></i> Finalizar Compra</button>
</div>

<!-- MODAL PAGAMENTO -->
<div class="modal" id="modalPagamento">
  <div class="modal-content" id="modalConteudo">
    <h3>Escolha a forma de pagamento</h3>
    <p>Total: R$ <span id="totalModal">0.00</span></p>
    <div id="formasPagamento">
      <button id="pix" onclick="mostrarPix()">PIX <i class="fa-solid fa-qrcode"></i></button>
      <button id="cartao" onclick="mostrarCartao()">Cartão <i class="fa-solid fa-credit-card"></i></button>
    </div>
    <button id="fecharModal" onclick="fecharModal()">Fechar</button>
  </div>
</div>

<footer id="contato">
<p><i class="fa-solid fa-envelope"></i> cleonisemiranda543@gmail.com</p>
<p>&copy; 2025 Loja de Roupas Samuel</p>
</footer>

<script>
let carrinho=[];

function adicionarCarrinho(nome,preco){carrinho.push({nome,preco}); atualizarCarrinho();}
function removerItem(i){carrinho.splice(i,1); atualizarCarrinho();}
function atualizarCarrinho(){
  const itens=document.getElementById('itens-carrinho');
  const totalElem=document.getElementById('total');
  const countElem=document.getElementById('carrinho-count');
  itens.innerHTML='';
  let total=0;
  carrinho.forEach((item,i)=>{
    total+=item.preco;
    const div=document.createElement('div');
    div.className='carrinho-item';
    div.innerHTML=`${item.nome} - R$ ${item.preco.toFixed(2)} <button onclick="removerItem(${i})"><i class="fa-solid fa-trash"></i></button>`;
    itens.appendChild(div);
  });
  totalElem.textContent=total.toFixed(2);
  countElem.textContent=carrinho.length;
}
function toggleCarrinho(){const c=document.getElementById('carrinho'); c.style.display=c.style.display==='none'?'block':'none';}
function abrirPagamento(){
  if(carrinho.length===0){alert("O carrinho está vazio!");return;}
  const total=carrinho.reduce((acc,i)=>acc+i.preco,0);
  document.getElementById('totalModal').textContent=total.toFixed(2);
  document.getElementById('modalPagamento').style.display='flex';
  document.getElementById('formasPagamento').style.display='block';
}
function fecharModal(){document.getElementById('modalPagamento').style.display='none';}

/* PIX */
function mostrarPix(){
  document.getElementById('modalConteudo').innerHTML=`
  <h3>Pagamento via PIX</h3>
  <p>Total: R$ ${carrinho.reduce((acc,i)=>acc+i.preco,0).toFixed(2)}</p>
  <img src="https://via.placeholder.com/200x200?text=QR+Code+PIX" alt="QR Code PIX">
  <br><button id="confirm" onclick="confirmarCompra()">Confirmar Pagamento</button>
  <button id="fecharModal" onclick="fecharModal()">Fechar</button>`;
}

/* CARTÃO */
function mostrarCartao(){
  document.getElementById('modalConteudo').innerHTML=`
  <h3>Pagamento com Cartão</h3>
  <p>Total: R$ ${carrinho.reduce((acc,i)=>acc+i.preco,0).toFixed(2)}</p>
  <input type="text" placeholder="Número do Cartão"><br>
  <input type="text" placeholder="Validade MM/AA"><br>
  <input type="text" placeholder="CVV"><br>
  <button id="confirm" onclick="confirmarCompra()">Confirmar Pagamento</button>
  <button id="fecharModal" onclick="fecharModal()">Fechar</button>`;
}

/* CONFIRMAÇÃO COM CONFETE */
function confirmarCompra(){
  carrinho=[];
  atualizarCarrinho();
  fecharModal();
  criarConfete(100);
  alert("Pagamento confirmado! Obrigado pela compra.");
}

function criarConfete(qt){
  for(let i=0;i<qt;i++){
    const c=document.createElement('div');
    c.className='confete';
    c.style.left=Math.random()*100+'vw';
    c.style.background='hsl('+(Math.random()*360)+',100%,50%)';
    c.style.width=c.style.height=Math.random()*8+5+'px';
    document.body.appendChild(c);
    setTimeout(()=>c.remove(),3000);
  }
}
</script>
</body>
</html>
