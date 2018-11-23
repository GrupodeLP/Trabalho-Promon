# Trabalho-Promon

package promom;

import promom.ConexaoComMySQL;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;



public class CategoriaDAO {         
    private Connection conexao=null;

    public CategoriaDAO() {
    conexao = ConexaoComMySQL.getConexaoMySQL();
    }
    
   
    public boolean insert(Nome nome){ 
        String sql = "INSERT INTO nome (descricao) VALUES (?)";
        PreparedStatement statement = null;
        try{
        statement = conexao.prepareStatement(sql);
        statement.setString(1, nome.getDescricao());
        statement.executeUpdate();
        return true;
    }catch (SQLException e){
            System.err.println("Erro: "+e);
            return false;
    }finally{
           
            ConexaoComMySQL.FecharConexao(conexao, statement);
        }   
    }
    
   
    public List<Nome> select(){ 
         String sql = "SELECT * FROM categoria";
         PreparedStatement statement = null;
         ResultSet resultset = null;
         List<Nome> categorias = new ArrayList<>();
         try{
             statement = conexao.prepareStatement(sql);
             resultset = statement.executeQuery();
             while(resultset.next()){
                 Nome categoria = new Nome();
                 categoria.setDescricao(resultset.getString("descricao"));
                 categorias.add(categoria);
             }
         }catch(SQLException e ){
             System.out.println("erro "+e);
         }
         finally{
             ConexaoComMySQL.FecharConexao();
         }
        List<Nome> nomes = null;
         return nomes;
    }
    
  
    public boolean update (Nome nome){ 
        String sql = "UPDATE categoria SET descricao = ? WHERE id= ?";
        PreparedStatement statement = null;
        try{
        statement = conexao.prepareStatement(sql);
        statement.setString(1, nome.getDescricao());
        statement.setInt(2, nome.getId());
        statement.executeUpdate();
        return true;
    }catch (SQLException e){
            System.out.println("erro: "+e);
            return false;
    }finally{
           
            ConexaoComMySQL.FecharConexao();
        }
    }
    
    
    public boolean delete (Nome nome){
        String sql = "DELETE FROM categoria WHERE id = ?";
        PreparedStatement statement = null;
        try{
        statement = conexao.prepareStatement(sql);
        statement.setInt(1, nome.getId());
        statement.executeUpdate();
        return true;
    }catch (SQLException e){
            System.out.println("erro: "+e);
            return false;
    }finally{
           
            ConexaoComMySQL.FecharConexao();
        }
    }

    private static class Nome {

        public Nome() {
        }

        private String getDescricao() {
            throw new UnsupportedOperationException(); 
        }

        private void setDescricao(String string) {
            throw new UnsupportedOperationException(); 
        }

        private int getId() {
            throw new UnsupportedOperationException(); 
        }

        
        
    }
}
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package exceptionhandling;

/**
 *
 * @author Aluno
 */
import java.util.InputMismatchException;
import java.util.Scanner;

public class ExceptionHandling {

    public static void main(String[] args) {
        // TODO code application logic here
        Scanner read = new Scanner(System.in);

        int division;
        try {
            System.out.println("enter a number");
            int number1 = read.nextInt();
            System.out.println("enter a second number");
            int number2 = read.nextInt();
            division = number1 / number2;
        } catch (ArithmeticException e) {
            System.out.println("You tried to divide by zero");
            System.out.println("erro :" + e);
            division = 0;
        }
        catch (InputMismatchException e){
            System.out.println("you entered the wrong type");
            System.out.println("error: "+e);
            division=0;
        }
        System.out.println("division: " + division);
        //ArithmeticException
        //InputMismatchException
    }

}
