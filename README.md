Estructuras
===========
package BancoSemaforo;


import java.util.ArrayList;

public class BankUser extends Thread 
	{

		public BankUser(ArrayList<Integer> newOperations, String myName)
		{
			this.operations = newOperations;
			this.myName = myName;
		}
		
		public void waiting()
		{
			try 
			{
				this.wait(50);
			} catch (Exception e) 
			{
				//e.printStackTrace();
				System.out.println("Panic!");
			}
		}
		
		@Override
	    public void run() 
	    {
	        for(int variableInFor = 0; variableInFor < operations.size(); variableInFor++)
	        {
	        	Banco.waiter();
	        	int temp = Banco.bankBalance;
	        	temp = temp + operations.get(variableInFor);
	        	Banco.bankBalance = temp;
	        	Banco.signal();
	        }
	    }
	    
	    ArrayList<Integer> operations;
	    String myName;
	}
