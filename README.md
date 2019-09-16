Aluguel

public class Aluguel {
	private Fita fita;
    private int tempoAlugado;

    public Aluguel(Fita fita, int tempoAlugado) {
        this.fita = fita;
        this.tempoAlugado = tempoAlugado;
    }
    
    public double obterSubtotal(){
		double subTotal = fita.obterValorFita();	
		if(tempoAlugado > fita.obterDiasFita()){
			subTotal += (tempoAlugado- fita.obterDiasFita()) 
					* fita.obterValorMultaFita();
		}
		return subTotal;
	}
    
    public Fita getFita() {
        return fita;
    }
    
    public void setFita(Fita fita) {
		this.fita = fita;
	}
    
    public int getDiasAlugada() {
        return tempoAlugado;
    }
    
    public void setDiasAlugada(int tempoAlugado) {
		this.tempoAlugado = tempoAlugado;
	}
    
}



Cliente

import java.util.ArrayList;
import java.util.Collection;

public class Cliente {
    private String name;

    private Collection<Aluguel> fitasLocadas = new ArrayList<Aluguel>();

    public Cliente(String nome) {
        this.name = name;
    }

    public String getNome() {
        return name;
    }

    public void adicionaAluguel(Aluguel aluguel) {
        fitasLocadas.add(aluguel);
    }

    public String extrato() {
        final String fimDeLinha = System.getProperty("line.separator");
        double valorTotal = 0.0;
        int pontosDeAlugadorFrequente = 0;
        String resultado = "Registro de Alugueis de " + getNome() + fimDeLinha;

        for (Aluguel f : fitasLocadas) {

            double valorCorrente = f.obterSubtotal();
            	pontosDeAlugadorFrequente++;
            	
            	if (f.getFita().getCodigoDePreco() == Fita.Tipo.lancamento
                        && f.getDiasAlugada() > 1) {
                        pontosDeAlugadorFrequente++;
                    
            } 

            resultado += "\t" + f.getFita().getTitulo() + "\t"
                    + valorCorrente + fimDeLinha;
            valorTotal += valorCorrente;
        } 
        
        resultado += "Valor total devido: " + valorTotal + fimDeLinha;
        resultado += "Voce acumulou " + pontosDeAlugadorFrequente
                     + " pontos de alugador frequente";
        return resultado;
    }
}



Fita
public class Fita {
	
	public enum Tipo {
		 normal, lancamento, infantil
	}
	
    private String titulo;
    private Tipo codigoDePreco;

    public Fita(String titulo, Tipo codigoDePreco) {
        this.titulo = titulo;
        this.codigoDePreco = codigoDePreco;
    }
    
    public double obterValorMultaFita(){
		double valorRetorno = 0.0;
		
		if(codigoDePreco.equals(Tipo.normal)){
			valorRetorno = 1.5;
		}else if(codigoDePreco.equals(Tipo.lancamento)){
			valorRetorno = 3.0;
		}else if(codigoDePreco.equals(Tipo.infantil)){
			valorRetorno = 1.5;
		}
				
		return valorRetorno;
	}
	
	public double obterValorFita(){
		double valorRetorno = 0.0;
		
		if(codigoDePreco.equals(Tipo.normal)){
			valorRetorno = 2.0;
		}else if(codigoDePreco.equals(Tipo.lancamento)){
			valorRetorno = 3.0;
		}else if(codigoDePreco.equals(Tipo.infantil)){
			valorRetorno = 1.5;
		}
				
		return valorRetorno;
	}
	
	public int obterDiasFita(){
		
		int  diasFita = 0;		
		if(codigoDePreco.equals(Tipo.normal)){
			 diasFita =2;
		}else if(codigoDePreco.equals(Tipo.lancamento)){
			diasFita =1;
		}else if(codigoDePreco.equals(Tipo.infantil)){
			diasFita =3;
		}			
		return diasFita;
	}
	
    public String getTitulo() {
        return titulo;
    }
    
    public void setTitulo(String titulo) {
		this.titulo = titulo;
	}
    
    public Tipo getCodigoDePreco() {
        return codigoDePreco;
    }

    public void setCodigoDePrevo(Tipo codigoDePreco) {
        this.codigoDePreco = codigoDePreco;
    }
}
