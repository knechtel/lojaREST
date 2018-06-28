# lojaREST



Aplicação que utiliza REST para troca de mensagem(XML), tem um banco de dados simulado, utiliza Jersey e glashfish, JUnit e Xstream.

é implementado um cliente e um Servidor.


Pedaço de código que representa o serviço de carrinho
```Java

@Path("carrinhos")
public class CarrinhoResource {
	@GET
	@Produces(MediaType.APPLICATION_XML)
	public String busca() {
	    Carrinho carrinho = new CarrinhoDAO().busca(1l);
	    return carrinho.toXML();
	}
}
```



Teste unitário serve para simular um cliente consumindo recurso.

```Java
    @Before
    public void before() {
      
        this.server =Servidor.inicializaServidor();
    }

    @After
    public void mataServidor() {
        server.stop();
    }

    @Test
    public void testaQueBuscarUmCarrinhoTrazOCarrinhoEsperado() {
        Client client = ClientBuilder.newClient();
        WebTarget target = client.target("http://localhost:8080");
        String conteudo = target.path("/carrinhos").request().get(String.class);
        Carrinho carrinho = (Carrinho) new XStream().fromXML(conteudo);
        Assert.assertEquals("Rua Vergueiro 3185, 8 andar", carrinho.getRua());
    }

}

```
