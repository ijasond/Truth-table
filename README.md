import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.regex.Pattern;

import javax.swing.event.*;

public class TablePanel extends JPanel {

	private int width, height;
	private JPanel main, top, bottom, sub, command;
	private JButton enter, reset, back, p, q, r, neg, or ,and, imp, open, close, xor;
	private JTextArea eq, output;
	
	public TablePanel()
	{
		
		//command buttons, textArea 
		enter = new JButton("Enter");
		enter.addActionListener(new ButtonListener());
		reset = new JButton("Reset");
		reset.addActionListener(new ButtonListener());
		eq = new JTextArea();
		output = new JTextArea();
		
		//variable buttons
		p = new JButton("p");
		p.addActionListener(new ButtonListener());
		q = new JButton("q");
		q.addActionListener(new ButtonListener());
		r = new JButton("r");
		r.addActionListener(new ButtonListener());
		
		//propositional logic
		neg = new JButton("NOT");
		neg.addActionListener(new ButtonListener());
		or = new JButton("OR");
		or.addActionListener(new ButtonListener());
		and = new JButton("AND");
		and.addActionListener(new ButtonListener());
		imp = new JButton("IMPLIES");
		imp.addActionListener(new ButtonListener());
		
		
		//parenthesis and backspace
		open = new JButton("(");
		open.addActionListener(new ButtonListener());
		close = new JButton(")");
		close.addActionListener(new ButtonListener());
		back = new JButton("backspace");
		back.addActionListener(new ButtonListener());
		
		//command calculator top JPanel
		command = new JPanel(new GridLayout(2,5));
		command.add(p);
		command.add(q);
		command.add(r);
		command.add(neg);
		command.add(imp);
		command.add(open);
		command.add(close);
		command.add(and);
		command.add(or);
		
		
		
		//sub panel consists of enter, backspace and reset buttons
		sub = new JPanel();
		sub.setLayout(new GridLayout(1,3));
		sub.add(enter);
		sub.add(back);
		sub.add(reset);
		
		//top panel consists of sub and text area
		top = new JPanel(new GridLayout(3,1));
		top.add(eq);
		top.add(command);
		top.add(sub);
	
		
		//bottom panel consists of the generated truth table from the top panel
		bottom = new JPanel(new GridLayout(1,1));
		bottom.add(output);
		
		
		//main panel, combination of top and bottom panel
		main = new JPanel();
		main.setLayout(new GridLayout(2,1));
		main.add(top);
		main.add(bottom);
		add(main);
	}
	
	
	
	private class ButtonListener implements ActionListener
	{
		public void actionPerformed(ActionEvent event)
		{
			 JButton buttonX = (JButton) event.getSource();
			
			 if(buttonX == p){
				 eq.setText(eq.getText() + "p");
			 }
			 
			 if (buttonX == q){
				 eq.setText(eq.getText()+ "q");
			 }
			
			 if (buttonX == r){
				 eq.setText(eq.getText() + "r");
			 }
		     
			 if (buttonX == neg){
		    	 eq.setText(eq.getText() + "~");
		     }
		    
			 if (buttonX == and){
		    	 eq.setText(eq.getText() + "^");
		     }
			 if (buttonX == or){
				 eq.setText(eq.getText() + "v");
			 }
			 if (buttonX == imp){
				 eq.setText(eq.getText() + "->");
			 }
			 if (buttonX == open){
				 eq.setText(eq.getText() + "(");
			 }
			 if (buttonX == close){
				 eq.setText(eq.getText() + ")");
			 }
			 if (buttonX == xor){
				 eq.setText(eq.getText() + "<->");
			 }
				 
			 if (buttonX == back){
				 if(eq.getText() != null)
				 {
					 String eq1 = eq.getText();
					 eq.setText(eq1.substring(0, eq1.length()-1));	 
				 }
			 }
			 
			if (buttonX == reset){
				eq.setText(null);
				output.setText(null);
			}
			
			
			 boolean a, b, c;
		       String text = eq.getText(); 
		 if (buttonX == enter ){	//enter button
			 
			 //single variable 
			 if (text.equals("p")){
				 a = false;
				 System.out.println("p");
				 output.setText("p");
				 do {
					 System.out.println(a);
					 output.setText(output.getText() + "\n" + a);
					 a = !a;
				 } while (a);
			 }
			 
			 if (text.equals("q")){
				 a = false;
				 System.out.println("q");
				 output.setText("q");
				 do {
					 System.out.println(a);
					 output.setText(output.getText() + "\n" + a);
					 a = !a;
				 } while (a);
			 }
			 
			 if (text.equals("r")){
				 a = false;
				 System.out.println("r");
				 output.setText("r");
				 do {
					 System.out.println(a);
					 output.setText(output.getText() + "\n" + a);
					 a = !a;
				 } while (a);
			 }
			 
			 if (text.equals("~p")){
				 a = false;
				 System.out.println("p\t~p");
				 output.setText("p\t~p");
				 do {
					 System.out.println(a + "\t" + !a);
					 output.setText(output.getText() + "\n" + a + "\t" + !a);
					 a = !a;
				 } while (a);
			 }
				 
			 if (text.equals("~q")){
				 a = false;
				 System.out.println("q\t~q");
				 output.setText("q\t~q");
				 do {
					 System.out.println(a + "\t" + !a);
					 output.setText(output.getText() + "\n" + a + "\t" + !a);
					 a = !a;
				 } while (a);
			 }
			 
			 if (text.equals("~r")){
				 a = false;
				 System.out.println("r\t~r");
				 output.setText("r\t~r");
				 do {
					 System.out.println(a + "\t" + !a);
					 output.setText(output.getText() + "\n" + a + "\t" + !a);
					 a = !a;
				 } while (a);
			 }
			 
			 //end of single variable
				 
			 // Two variable cases
		        
		       if (text.equals("p^q") || text.equals("q^p") ){	// p AND q
		                    a = false;
		                    System.out.println("p\tq\tp and q");
		                    output.setText("p\tq\tp and q");
		                    do {
		                          b = false;
		                          do {
		                                System.out.println(a + "\t" + b + "\t" + (a && b));
		                                output.setText(output.getText()+ "\n" + a + "\t" + b + "\t" + (a && b));
		                                b = !b;
		                          } while (b);
		                          a = !a;
		                    } while (a);
		       }

		       else if (text.equals("pvq") || text.equals( "qvp")){  // p OR q
		                    a = false;
		                    System.out.println("p\tq\tp or q");
		                    output.setText("p\tq\tp or q");
		                    do {
		                          b = false;
		                          do {
		                                System.out.println(a + "\t" + b + "\t" + (a || b));
		                                output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + (a || b));
		                                b = !b;
		                          } while (b);
		                          a = !a;
		                    } while (a);
		       }
		       
		       else if (text.equals("~p^q") || text.equals("q^~p")) {	// NOT p AND q
	                a = false;
	                System.out.println("p\tq\t~p\tnot p and q");
	                output.setText("p\tq\t~p\tnot p and q");
	                do {
	                      b = false;
	                      do {
	                            System.out.println(a + "\t" + b + "\t" + !a + "\t" + (!a && b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !a + "\t" + (!a && b));
	                            b = !b;
	                      } while (b);
	                      a = !a;
	                } while (a);
		       }
	    	
		       else if (text.equals("p^~q") || text.equals( "~q^p")) {	// p AND NOT q
	                a = false;
	                System.out.println("p\tq\t~q\tp and not q");
	                output.setText("p\tq\t~q\tp and not q");
	                do {
	                      b = false;
	                      do {
	                            System.out.println(a + "\t" + b + "\t" + !b + "\t" + (a && !b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !b + "\t" + (a && !b));
	                            b = !b;
	                      } while (b);
	                      a = !a;
	                } while (a);
		       }
	    	
	           else if (text.equals("~p^~q") || text.equals("~q^~p")) {	// NOT p AND NOT q
	                a = false;
	                System.out.println("p\tq\t~p\t~q\tnot p & not q");
	                output.setText("p\tq\t~p\t~q\tnot p & not q");
	                do {
	                	  b = false;
	                	  do {
	                			System.out.println(a + "\t" + b + "\t" + !a + "\t" + !b + "\t" + (!a && !b));
	                			output.setText(output.getText()+ "\n" + a + "\t" + b + "\t" + !a + "\t" + !b + "\t" + (!a && !b));
	                			b = !b;
	                	  } while (b);
	                	  a = !a;
	                } while (a);
	           }

	           else if (text.equals("~pvq") || text.equals("qv~p")) { 	// NOT p OR q
	                a = false;
	                System.out.println("p\tq\t~p\tnot p or q");
	                output.setText("p\tq\t~p\tnot p or q");
	                do {
	                      b = false;
	                      do {
	                            System.out.println(a + "\t" + b + "\t" + !a + "\t" + (!a || b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !a + "\t" + (!a || b));
	                            b = !b;
	                      } while (b);
	                      a = !a;
	                } while (a);
	           }
	               
	           else if (text.equals("pv~q") || text.equals("~qvp")) {	// p OR NOT q
	                a = false;
	                System.out.println("p\tq\t~q\tp or not q");
	                output.setText("p\tq\t~q\tp or not q");
	                do {
	                      b = false;
	                      do {
	                            System.out.println(a + "\t" + b + "\t" + !b + "\t" + (a || !b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !b + "\t" + (a || !b));
	                            b = !b;
	                      } while (b);
	                      a = !a;
	                } while (a);
	           }
	           
	           else if (text.equals("~pv~q") || text.equals("~qv~p")) {	// NOT p OR NOT q
	        	    a = false;
	        	    System.out.println("p\tq\t~p\t~q\tnot p or not q");
	        	    output.setText("p\tq\t~p\t~q\tnot p or not q");
	        	    do {
	        	    	  b = false;
	        	    	  do {
	        	    		  	System.out.println(a + "\t" + b + "\t" + !a + "\t" + !b + "\t" + (!a || !b));
	        	    		  	output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !a + "\t" + !b + "\t" + (!a || !b));
	        	    		  	b = !b;
	        	    	  } while (b);
	        	    	  a = !a;
	        	    } while (a);
	           }
		       
	           else if (text.equals("p->q")) {       // p IMPLIES q  
	                a = false;
	                System.out.println("p\tq\tp implies q");
	                output.setText("p\tq\tp implies q");
	                do {
	                      b = false;
	                      do {
	                            System.out.println(a + "\t" + b + "\t" + (!a || b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + (!a || b));
	                            b = !b;
	                      } while (b);
	                      a = !a;
	                } while (a);
	           }
		       
	           else if (text.equals("~p->q")) {  	// NOT p IMPLIES q
	                a = false;
	                System.out.println("p\tq\t~p\tnot p implies q");
	                output.setText("p\tq\t~p\tnot p implies q");
	                do {
	                      b = false;
	                      do {
	                            System.out.println(a + "\t" + b + "\t" + !a + "\t" + (a || b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !a + "\t" + (a || b));
	                            b = !b;
	                      } while (b);
	                      a = !a;
	                } while (a);
	           }
		       
	           else if (text.equals("p->~q")) {		// p IMPLIES NOT q
	        	   	a = false;
	        	   	System.out.println("p\tq\t~q\tp implies not q");
	        	   	output.setText("p\tq\t~q\tp implies not q");
	        	   	do {
	        	   		  b = false;
	        	   		  do {
	        	   			  	System.out.println(a + "\t" + b + "\t" + !b + "\t" + (!a || !b));
	        	   			  	output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !b + "\t" + (!a || !b));
	        	   			  	b = !b;
	        	   		  } while (b);
	        	   		  a = !a;
	        	   	} while (a);
	           }
		       
	           else if (text.equals("~p->~q")){ 	// NOT p IMPLIES NOT q
	        	    a = false;
	        	    System.out.println("p\tq\t~p\t~q\tnot p implies not q");
	        	    output.setText("p\tq\t~p\t~q\tnot p implies not q");
	        	    do {
	        	    	b = false;
	        	    	do{
	        	    		System.out.println(a + "\t" + b + "\t" + !a + "\t" + !b + "\t" + (a || !b));
	        	    		output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !a + "\t" + !b + "\t" + (a || !b));
	        	    		b = !b;
	        	    	} while (b);
	        	    	a = !a;
	        	    } while (a);
	           }

	           else if (text.equals("q->p")) {		// q IMPLIES p
	                a = false;
	                System.out.println("p\tq\tq implies p");
	                output.setText("p\tq\tq implies p");
	                do {
	                      b = false;
	                      do {
	                            System.out.println(a + "\t" + b + "\t" + (a || !b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + (a || !b));
	                            b = !b;
	                      } while (b);
	                      a = !a;
	                } while (a);
	           }
	
	           else if (text.equals("~q->p")) {		// NOT q IMPLIES p
	                a = false;
	                System.out.println("p\tq\t~q\tnot q implies p");
	                output.setText("p\tq\t~q\tnot q implies p");
	                do {
	                      b = false;
	                      do {
	                            System.out.println(a + "\t" + b + "\t" + !b + "\t" + (a || b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !b + "\t" + (a || b));
	                            b = !b;
	                      } while (b);
	                      a = !a;
	                } while (a);
	           }
	           
	           else if (text.equals("q->~p") ) {	// q IMPLIES NOT p
	        	    a = false;
	        	    System.out.println("p\tq\t~p\tq implies not p");
	        	    output.setText("p\tq\t~p\tq implies not p");
	        	    do {
	        	    	  b = false;
	        	    	  do {
	        	    		  	System.out.println(a + "\t" + b + "\t" + !a + "\t" + (!a || !b));
	        	    		  	output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !a + "\t" + (!a || !b));
	        	    		  	b = !b;
	        	    	  } while (b);
	        	    	  a = !a;
	        	    } while (a);
	           }
		       
	           else if (text.equals("~q->~p")) {		// q IMPLIES p
	                a = false;
	                System.out.println("p\tq\t~p\t~q\tnot q implies not p");
	                output.setText("p\tq\t~p\t~q\tnot q implies not p");
	                do {
	                      b = false;
	                      do {
	                            System.out.println(a + "\t" + b + "\t" + !a + "\t" + !b + "\t" + (!a || b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + !a + "\t" + !b + "\t" + (!a || b));
	                            b = !b;
	                      } while (b);
	                      a = !a;
	                } while (a);
	           }
	           
		       //End of two variable cases
		       
		       //Three variable cases
		       
		       //3 OR
		       if (text.equals("pvqvr") || text.equals("pvrvq") || text.equals("qvpvr") || text.equals("qvrvp") || text.equals("rvpvq") || text.equals("rvqvp") ||
		    	   text.equals("(pvq)vr") || text.equals("(pvr)vq") || text.equals("(qvp)vr") || text.equals("(qvr)vp") || text.equals("(rvp)vq") || text.equals("(rvq)vp") ||
		    	   text.equals("pv(qvr)") || text.equals("pv(rvq)") || text.equals("qv(pvr)") || text.equals("qv(rvp)") || text.equals("rv(pvq)") || text.equals("rv(qvp)")){
		    	   a = false;
		    	   System.out.println("p\tq\tr\t" + eq.getText());
		    	   output.setText("p\tq\tr\t" + eq.getText());
		    	   do {
		    		   b = false;
		    		   do {
		    			   c = false;
		    			   do {
		    				   System.out.println(a + "\t" + b + "\t" + c + "\t" +(a || b ||c));
		    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" +(a || b ||c));
		    				   c = !c;
		    			   }while (c);
		    			   b = !b;
		    		   }while (b);
		    		   a = !a;
		    	   }while (a);
		       }
		       
		       //3 OR not p
		       if (text.equals("~pvqvr") || text.equals("~pvrvq") || text.equals("qv~pvr") || text.equals("qvrv~p") || text.equals("rv~pvq") || text.equals("rvqv~p") ||
			    	   text.equals("(~pvq)vr") || text.equals("(~pvr)vq") || text.equals("(qv~p)vr") || text.equals("(qvr)v~p") || text.equals("(rv~p)vq") || text.equals("(rvq)v~p") ||
			    	   text.equals("~pv(qvr)") || text.equals("~pv(rvq)") || text.equals("qv(~pvr)") || text.equals("qv(rv~p)") || text.equals("rv(~pvq)") || text.equals("rv(qv~p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~p\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~p\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a || b ||c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a || b ||c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 OR not q
		       if (text.equals("pv~qvr") || text.equals("pvrv~q") || text.equals("~qvpvr") || text.equals("~qvrvp") || text.equals("rvpv~q") || text.equals("rv~qvp") ||
			    	   text.equals("(pv~q)vr") || text.equals("(pvr)v~q") || text.equals("(~qvp)vr") || text.equals("(~qvr)vp") || text.equals("(rvp)v~q") || text.equals("(rv~q)vp") ||
			    	   text.equals("pv(~qvr)") || text.equals("pv(rv~q)") || text.equals("~qv(pvr)") || text.equals("~qv(rvp)") || text.equals("rv(pv~q)") || text.equals("rv(~qvp)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~q\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~q\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a || !b ||c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a || !b ||c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       //3 OR not r
		       if (text.equals("pvqv~r") || text.equals("pv~rvq") || text.equals("qvpv~r") || text.equals("qv~rvp") || text.equals("~rvpvq") || text.equals("~rvqvp") ||
			    	   text.equals("(pvq)v~r") || text.equals("(pv~r)vq") || text.equals("(qvp)v~r") || text.equals("(qv~r)vp") || text.equals("(~rvp)vq") || text.equals("(~rvq)vp") ||
			    	   text.equals("pv(qv~r)") || text.equals("pv(~rvq)") || text.equals("qv(pv~r)") || text.equals("qv(~rvp)") || text.equals("~rv(pvq)") || text.equals("~rv(qvp)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~r\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~r\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a || b || !c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a || b || !c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 OR not q,p
		       if (text.equals("~pv~qvr") || text.equals("~pvrv~q") || text.equals("~qv~pvr") || text.equals("~qvrv~p") || text.equals("rv~pv~q") || text.equals("rv~qv~p") ||
			    	   text.equals("(~pv~q)vr") || text.equals("(~pvr)v~q") || text.equals("(~qv~p)vr") || text.equals("(~qvr)v~p") || text.equals("(rv~p)v~q") || text.equals("(rv~q)v~p") ||
			    	   text.equals("~pv(~qvr)") || text.equals("~pv(rv~q)") || text.equals("~qv(~pvr)") || text.equals("~qv(rv~p)") || text.equals("rv(~pv~q)") || text.equals("rv(~qv~p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~p\t~q\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~p\t~q\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a || !b ||c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a || !b ||c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 OR not p,r
		       if (text.equals("~pvqv~r") || text.equals("~pv~rvq") || text.equals("qv~pv~r") || text.equals("qv~rv~p") || text.equals("~rv~pvq") || text.equals("~rvqv~p") ||
			    	   text.equals("(~pvq)v~r") || text.equals("(~pv~r)vq") || text.equals("(qv~p)v~r") || text.equals("(qv~r)v~p") || text.equals("(~rv~p)vq") || text.equals("(~rvq)v~p") ||
			    	   text.equals("~pv(qv~r)") || text.equals("~pv(~rvq)") || text.equals("qv(~pv~r)") || text.equals("qv(~rv~p)") || text.equals("~rv(~pvq)") || text.equals("~rv(qv~p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~p\t~r\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~p\t~r\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a || b ||!c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a || b ||!c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 OR not q,r
		       if (text.equals("pv~qv~r") || text.equals("pv~rv~q") || text.equals("~qvpv~r") || text.equals("~qv~rvp") || text.equals("~rvpv~q") || text.equals("~rv~qvp") ||
			    	   text.equals("(pv~q)v~r") || text.equals("(pv~r)v~q") || text.equals("(~qvp)v~r") || text.equals("(~qv~r)vp") || text.equals("(~rvp)v~q") || text.equals("(~rv~q)vp") ||
			    	   text.equals("pv(~qv~r)") || text.equals("pv(~rv~q)") || text.equals("~qv(pv~r)") || text.equals("~qv(~rvp)") || text.equals("~rv(pv~q)") || text.equals("~rv(~qvp)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~q\t~r\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~q\t~r\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a || !b ||!c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a || !b ||!c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 OR negate all
		       if (text.equals("~pv~qv~r") || text.equals("~pv~rv~q") || text.equals("~qv~pv~r") || text.equals("~qv~rv~p") || text.equals("~rv~pv~q") || text.equals("~rv~qv~p") ||
			    	   text.equals("(~pv~q)v~r") || text.equals("(~pv~r)v~q") || text.equals("(~qv~p)v~r") || text.equals("(~qv~r)v~p") || text.equals("(~rv~p)v~q") || text.equals("(~rv~q)v~p") ||
			    	   text.equals("~pv(~qv~r)") || text.equals("~pv(~rv~q)") || text.equals("~qv(~pv~r)") || text.equals("~qv(~rv~p)") || text.equals("~rv(~pv~q)") || text.equals("~rv(~qv~p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~p\t~q\t~r\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~p\t~q\t~r\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!a || !b ||!c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!a || !b ||!c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 AND
		       else if (text.equals("p^q^r") || text.equals("p^r^q") || text.equals("q^p^r") || text.equals("q^r^p") || text.equals("r^p^q") || text.equals("r^q^p") ||
			    	   text.equals("(p^q)^r") || text.equals("(p^r)^q") || text.equals("(q^p)^r") || text.equals("(q^r)^p") || text.equals("(r^p)^q") || text.equals("(r^q)^p") ||
			    	   text.equals("p^(q^r)") || text.equals("p^(r^q)") || text.equals("q^(p^r)") || text.equals("q^(r^p)") || text.equals("r^(p^q)") || text.equals("r^(q^p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t" + eq.getText());
			    	   output.setText("p\tq\tr\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" +(a && b && c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" +(a && b && c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 AND not p
		       if (text.equals("~p^q^r") || text.equals("~p^r^q") || text.equals("q^~p^r") || text.equals("q^r^~p") || text.equals("r^~p^q") || text.equals("r^q^~p") ||
			    	   text.equals("(~p^q)^r") || text.equals("(~p^r)^q") || text.equals("(q^~p)^r") || text.equals("(q^r)^~p") || text.equals("(r^~p)^q") || text.equals("(r^q)^~p") ||
			    	   text.equals("~p^(q^r)") || text.equals("~p^(r^q)") || text.equals("q^(~p^r)") || text.equals("q^(r^~p)") || text.equals("r^(~p^q)") || text.equals("r^(q^~p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~p\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~p\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a && b && c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a && b && c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 AND not q
		       if (text.equals("p^~q^r") || text.equals("p^r^~q") || text.equals("~q^p^r") || text.equals("~q^r^p") || text.equals("r^p^~q") || text.equals("r^~q^p") ||
			    	   text.equals("(p^~q)^r") || text.equals("(p^r)^~q") || text.equals("(~q^p)^r") || text.equals("(~q^r)^p") || text.equals("(r^p)^~q") || text.equals("(r^~q)^p") ||
			    	   text.equals("p^(~q^r)") || text.equals("p^(r^~q)") || text.equals("~q^(p^r)") || text.equals("~q^(r^p)") || text.equals("r^(p^~q)") || text.equals("r^(~q^p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~q\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~q\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a && !b && c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a && !b && c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
		       }
		       
		       //3 AND not r
		       if (text.equals("p^q^~r") || text.equals("p^~r^q") || text.equals("q^p^~r") || text.equals("q^~r^p") || text.equals("~r^p^q") || text.equals("~r^q^p") ||
			    	   text.equals("(p^q)^~r") || text.equals("(p^~r)^q") || text.equals("(q^p)^~r") || text.equals("(q^~r)^p") || text.equals("(~r^p)^q") || text.equals("(~r^q)^p") ||
			    	   text.equals("p^(q^~r)") || text.equals("p^(~r^q)") || text.equals("q^(p^~r)") || text.equals("q^(~r^p)") || text.equals("~r^(p^q)") || text.equals("~r^(q^p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~r\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~r\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a && b && !c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a && b && !c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
		       }
		       
		       //3 AND not p and q
		       if (text.equals("~p^~q^r") || text.equals("~p^r^~q") || text.equals("~q^~p^r") || text.equals("~q^r^~p") || text.equals("r^~p^~q") || text.equals("r^~q^~p") ||
			    	   text.equals("(~p^~q)^r") || text.equals("(~p^r)^~q") || text.equals("(~q^~p)^r") || text.equals("(~q^r)^~p") || text.equals("(r^~p)^~q") || text.equals("(r^~q)^~p") ||
			    	   text.equals("~p^(~q^r)") || text.equals("~p^(r^~q)") || text.equals("~q^(~p^r)") || text.equals("~q^(r^~p)") || text.equals("r^(~p^~q)") || text.equals("r^(~q^~p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~p\t~q\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~p\t~q\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a && !b && c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a && b && c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 AND not p and r
		       if (text.equals("~p^q^~r") || text.equals("~p^~r^q") || text.equals("q^~p^~r") || text.equals("q^~r^~p") || text.equals("~r^~p^q") || text.equals("~r^q^~p") ||
			    	   text.equals("(~p^q)^~r") || text.equals("(~p^~r)^q") || text.equals("(q^~p)^~r") || text.equals("(q^~r)^~p") || text.equals("(~r^~p)^q") || text.equals("(~r^q)^~p") ||
			    	   text.equals("~p^(q^~r)") || text.equals("~p^(~r^q)") || text.equals("q^(~p^~r)") || text.equals("q^(~r^~p)") || text.equals("~r^(~p^q)") || text.equals("~r^(q^~p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~p\t~r\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~p\t~r\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a && b && !c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a && b && !c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 AND not q and r 
		       if (text.equals("p^~q^~r") || text.equals("p^~r^~q") || text.equals("~q^p^~r") || text.equals("~q^~r^p") || text.equals("~r^p^~q") || text.equals("~r^~q^p") ||
			    	   text.equals("(p^~q)^~r") || text.equals("(p^~r)^~q") || text.equals("(~q^p)^~r") || text.equals("(~q^~r)^p") || text.equals("(~r^p)^~q") || text.equals("(~r^~q)^p") ||
			    	   text.equals("p^(~q^~r)") || text.equals("p^(~r^~q)") || text.equals("~q^(p^~r)") || text.equals("~q^(~r^p)") || text.equals("~r^(p^~q)") || text.equals("~r^(~q^p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~q\t~r\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~q\t~r\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a && !b && !c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a && !b && !c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 AND negate all
		       if (text.equals("~p^~q^~r") || text.equals("~p^~r^~q") || text.equals("~q^~p^~r") || text.equals("~q^~r^~p") || text.equals("~r^~p^~q") || text.equals("~r^~q^~p") ||
			    	   text.equals("(~p^~q)^~r") || text.equals("(~p^~r)^~q") || text.equals("(~q^~p)^~r") || text.equals("(~q^~r)^~p") || text.equals("(~r^~p)^~q") || text.equals("(~r^~q)^~p") ||
			    	   text.equals("~p^(~q^~r)") || text.equals("~p^(~r^~q)") || text.equals("~q^(~p^~r)") || text.equals("~q^(~r^~p)") || text.equals("~r^(~p^~q)") || text.equals("~r^(~q^~p)")){
			    	   a = false;
			    	   System.out.println("p\tq\tr\t~p\t~q\t~r\t" + eq.getText());
			    	   output.setText("p\tq\tr\t~p\t~q\t~r\t" + eq.getText());
			    	   do {
			    		   b = false;
			    		   do {
			    			   c = false;
			    			   do {
			    				   System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!a && !b && !c));
			    				   output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!a && b && c));
			    				   c = !c;
			    			   }while (c);
			    			   b = !b;
			    		   }while (b);
			    		   a = !a;
			    	   }while (a);
			       }
		       
		       //3 (p and q) or r
		       else if (text.equals("(p^q)vr") || text.equals("(q^p)vr") || text.equals("rv(p^q)") || text.equals("rv(q^p)")){
		    	   		a = false;
		    	   		System.out.println("p\tq\tr\tp^q\t" + eq.getText());
		    	   		output.setText("p\tq\tr\tp^q\t" + eq.getText());
		    	   		do {
		    	   			b = false;
		    	   			do {
		    	   				c = false;
		    	   				do {
		    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (a && b) + "\t" + ((a && b) || c));
		    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (a && b) + "\t" + ((a && b) || c));
		    	   					c = !c;
		    	   				}while(c);
		    	   				b = !b;
		    	   			}while(b);
		    	   			a =!a;
		    	   		}while(a);
		           }
		       
		       //3 (not p and q) or r
		       else if (text.equals("(~p^q)vr") || text.equals("(q^~p)vr") || text.equals("rv(~p^q)") || text.equals("rv(q^~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~p^q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~p^q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a && b) + "\t" + ((!a && b) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a && b) + "\t" + ((!a && b) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (p and not q) or r
		       else if (text.equals("(p^~q)vr") || text.equals("(~q^p)vr") || text.equals("rv(p^~q)") || text.equals("rv(~q^p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\tp^~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\tp^~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a && !b) + "\t" + ((a && !b) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a && !b) + "\t" + ((a && !b) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(not p and not q) or r
		       else if (text.equals("(~p^~q)vr") || text.equals("(~q^~p)vr") || text.equals("rv(~p^~q)") || text.equals("rv(~q^~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q\t~p^~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q\t~p^~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a && !b) + "\t" + ((!a && !b) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a && !b) + "\t" + ((!a && !b) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(p and q) or not r
		       else if (text.equals("(p^q)v~r") || text.equals("(q^p)v~r") || text.equals("~rv(p^q)") || text.equals("~rv(q^p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\tp^q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\tp^q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a && b) + "\t" + ((a && b) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a && b) + "\t" + ((a && b) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(p and not q) or not r
		       else if (text.equals("(p^~q)v~r") || text.equals("(~q^p)v~r") || text.equals("~rv(p^~q)") || text.equals("~rv(~q^p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\t~r\tp^~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\t~r\tp^~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a && !b) + "\t" + ((a && !b) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a && !b) + "\t" + ((a && !b) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(not p and q) or not r
		       else if (text.equals("(~p^q)v~r") || text.equals("(q^~p)v~r") || text.equals("~rv(~p^q)") || text.equals("~rv(q^~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~r\t~p^q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~r\t~p^q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a && b) + "\t" + ((!a && b) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a && b) + "\t" + ((!a && b) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(not p and not q) or not r
		       else if (text.equals("(~p^~q)v~r") || text.equals("(~q^~p)v~r") || text.equals("~rv(~p^~q)") || text.equals("~rv(~q^~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q\t~r\t~p^~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q\t~r\t~p^~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t"+ !b + "\t" + !c + "\t" + (!a && !b) + "\t" + ((!a && !b) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!a && !b) + "\t" + ((!a && !b) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (p and r) or q
		       else if (text.equals("(p^r)vq") || text.equals("(r^p)vq") || text.equals("qv(p^r)") || text.equals("qv(r^p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tp^r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tp^r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (a && c) + "\t" + ((a && c) || b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (a && c) + "\t" + ((a && c) || b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p and r) or q
		       else if (text.equals("(~p^r)vq") || text.equals("(r^~p)vq") || text.equals("qv(~p^r)") || text.equals("qv(r^~p)")){
	                a = false;
	                System.out.println("p\tq\tr\t~p\t~p^r\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\t~p^r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a && c) + "\t" + ((!a && c) || b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a && c) + "\t" + ((!a && c) || b));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (p and not r) or q
		       else if (text.equals("(p^~r)vq") || text.equals("(~r^p)vq") || text.equals("qv(p^~r)") || text.equals("qv(~r^p)")){
	                a = false;
	                System.out.println("p\tq\tr\t~r\tp^~r\t" + eq.getText());
	                output.setText("p\tq\tr\t~r\tp^~r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a && !c) + "\t" + ((a && !c) || b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a && !c) + "\t" + ((a && !c) || b));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (not p and not r) or q
		       else if (text.equals("(~p^~r)vq") || text.equals("(~r^~p)vq") || text.equals("qv(~p^~r)") || text.equals("qv(~r^~p)")){
	                a = false;
	                System.out.println("p\tq\tr\t~p\t~r\t~p^~r\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\t~r\t~p^~r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a && !c) + "\t" + ((!a && !c) || b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a && !c) + "\t" + ((!a && !c) || b));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (p and r) or not q
		       else if (text.equals("(p^r)v~q") || text.equals("(r^p)v~q") || text.equals("~qv(p^r)") || text.equals("~qv(r^p)")){
	                a = false;
	                System.out.println("p\tq\tr\t~q\tp^r\t" + eq.getText());
	                output.setText("p\tq\tr\t~q\tp^r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a && c) + "\t" + ((a && c) || !b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a && c) + "\t" + ((a && c) || !b));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (p and not r) or not q
		       else if (text.equals("(p^~r)v~q") || text.equals("(~r^p)v~q") || text.equals("~qv(p^~r)") || text.equals("~qv(~r^p)")){
	                a = false;
	                System.out.println("p\tq\tr\t~q\t~r\tp^~r\t" + eq.getText());
	                output.setText("p\tq\tr\t~q\t~r\tp^~r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a && !c) + "\t" + ((a && !c) || !b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a && !c) + "\t" + ((a && !c) || !b));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3(not p and r) or not q
		       else if (text.equals("(~p^r)v~q") || text.equals("(r^~p)v~q") || text.equals("~qv(~p^r)") || text.equals("~qv(r^~p)")){
	                a = false;
	                System.out.println("p\tq\tr\t~p\t~q\t~p^r\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\t~q\t~p^r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a && c) + "\t" + ((!a && c) || !b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a && c) + "\t" + ((!a && c) || !b));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 ( not p and not r) or not q
		       else if (text.equals("(~p^~r)v~q") || text.equals("(~r^~p)v~q") || text.equals("~qv(~p^~r)") || text.equals("~qv(~r^~p")){
	        	   a = false;
	                System.out.println("p\tq\tr\t~p\t~q\t~r\t~p^~r\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\t~q\t~r\t~p^~r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t"+ !b + "\t" + !c + "\t" + (!a && !c) + "\t" + ((!a && !c) || !b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!a && !c) + "\t" + ((!a && !c) || !b));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (q and r) or p
		       else if (text.equals("(q^r)vp") || text.equals("(r^q)vp") || text.equals("pv(q^r)") || text.equals("pv(r^q)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tq^r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tq^r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (b && c) + "\t" + ((b && c) || a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (b && c) + "\t" + ((b && c) || a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not q and r) or p
		       else if (text.equals("(~q^r)vp") || text.equals("(r^~q)vp") || text.equals("pv(~q^r)") || text.equals("pv(r^~q)")){
	                a = false;
	                System.out.println("p\tq\tr\t~q\t~q^r\t" + eq.getText());
	                output.setText("p\tq\tr\t~q\t~q^r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!b && c) + "\t" + ((!b && c) || a));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!b && c) + "\t" + ((!b && c) || a));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (q and not r) or p
		       else if (text.equals("(q^~r)vp") || text.equals("(~r^q)vp") || text.equals("pv(q^~r)") || text.equals("pv(~r^q)")){
	                a = false;
	                System.out.println("p\tq\tr\t~r\tq^~r\t" + eq.getText());
	                output.setText("p\tq\tr\t~r\tq^~r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (b && !c) + "\t" + ((b && !c) || a));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (b && !c) + "\t" + ((b && !c) || a));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (not q and not r) or p
		       else if (text.equals("(~q^~r)vp") || text.equals("(~r^~q)vp") || text.equals("pv(~q^~r)") || text.equals("pv(~r^~q)")){
	                a = false;
	                System.out.println("p\tq\tr\t~q\t~r\t~q^~r\t" + eq.getText());
	                output.setText("p\tq\tr\t~q\t~r\t~q^~r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (!b && !c) + "\t" + ((!b && !c) || a));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (!b && !c) + "\t" + ((!b && !c) || a));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3(q and r) or not p
		       else if (text.equals("(q^r)v~p") || text.equals("(r^q)v~p") || text.equals("~pv(q^r)") || text.equals("~pv(r^q)")){
	                a = false;
	                System.out.println("p\tq\tr\t~p\tq^r\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\tq^r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (b && c) + "\t" + ((b && c) || !a));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (b && c) + "\t" + ((b && c) || !a));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3(q and not r) or not p
		       else if (text.equals("(q^~r)v~p") || text.equals("(~r^q)v~p") || text.equals("~pv(q^~r)") || text.equals("~pv(~r^q)")){
	                a = false;
	                System.out.println("p\tq\tr\t~p\t~r\tq^~r\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\t~r\tq^~r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (b && !c) + "\t" + ((b && !c) || !a));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (b && !c) + "\t" + ((b && !c) || !a));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (not q and r) or not p
		       else if (text.equals("(~q^r)v~p") || text.equals("(r^~q)v~p") || text.equals("~pv(~q^r)") || text.equals("~pv(r^~q)")){
	                a = false;
	                System.out.println("p\tq\tr\t~p\t~q\t~q^r\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\t~q\t~q^r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!b && c) + "\t" + ((!b && c) || !a));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!b && c) + "\t" + ((!b && c) || !a));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (not q and not r) or not p
		       else if (text.equals("(~q^~r)v~p") || text.equals("(~r^~q)v~p") || text.equals("~pv(~q^~r)") || text.equals("~pv(~r^~q")){
	        	   a = false;
	                System.out.println("p\tq\tr\t~p\t~q\t~r\t~q^~r\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\t~q\t~r\t~q^~r\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t"+ !b + "\t" + !c + "\t" + (!c && !b) + "\t" + ((!c && !b) || !a));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!c && !b) + "\t" + ((!c && !b) || !a));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       
		       
		       //3 (p or q) and r
		       else if (text.equals("(pvq)^r") || text.equals("(qvp)^r") || text.equals("r^(pvq)") || text.equals("r^(qvp)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tpvq\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tpvq\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (a || b) + "\t" + ((a || b) && c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (a || b) + "\t" + ((a || b) && c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p or q) and r
		       else if (text.equals("(~pvq)^r") || text.equals("((qv~p)^r") || text.equals("r^(~pvq)") || text.equals("r^(qv~p)")){
	        	   a = false;
	                System.out.println("p\tq\tr\t~p\t~pvq\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\t~pvq\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a || b) + "\t" + ((!a || b) && c));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a || b) + "\t" + ((!a || b) && c));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }
		       
		       //3 (p or not q) and r
		       else if (text.equals("(pv~q)^r") || text.equals("(~qvp)^r") || text.equals("r^(pv~q)") || text.equals("r^(~qvp)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\tpv~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\tpv~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a && !b) + "\t" + ((a || !b) && c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a || !b) + "\t" + ((a || !b) && c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p or not q) and r
		       else if (text.equals("(~pv~q)^r") || text.equals("(~qv~p)^r") || text.equals("r^(~pv~q)") || text.equals("r^(~qv~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q\t~pv~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q\t~pv~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a || !b) + "\t" + ((!a || !b) && c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a || !b) + "\t" + ((!a || !b) && c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (p or q) and not r
		       else if (text.equals("(pvq)^~r") || text.equals("(qvp)^~r") || text.equals("~r^(pvq)") || text.equals("~r^(qvp)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\tpvq\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\tpvq\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a || b) + "\t" + ((a || b) && !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a || b) + "\t" + ((a || b) && !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (p or not q) and not r
		       else if (text.equals("(pv~q)^~r") || text.equals("(~qvp)^~r") || text.equals("~r^(pv~q)") || text.equals("~r^(~qvp)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\t~r\tpv~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\t~r\tpv~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a || !b) + "\t" + ((a || !b) && !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a || !b) + "\t" + ((a || !b) && !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p or q) and not r
		       else if (text.equals("(~pvq)^~r") || text.equals("(qv~p)^~r") || text.equals("~r^(~pvq)") || text.equals("~r^(qv~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~r\t~pvq\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~r\t~pvq\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a || b) + "\t" + ((!a || b) && !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a || b) + "\t" + ((!a || b) && !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p or not q) and not r
		       else if (text.equals("(~pv~q)^~r") || text.equals("(~qv~p)^~r") || text.equals("~r^(~pv~q)") || text.equals("~r^(~qv~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q\t~r\t~pv~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q\t~r\t~pv~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!a || !b) + "\t" + ((!a || !b) && !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t"  + !c + "\t" + (!a || !b) + "\t" + ((!a || !b) && !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       
		       //3 (p or r) and q
		       else if (text.equals("(pvr)^q") || text.equals("(rvp)^q") || text.equals("q^(pvr)") || text.equals("q^(rvp)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tpvr\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tpvr\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (a || c) + "\t" + ((a || c) && b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (a || c) + "\t" + ((a || c) && b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p or r) and q
		       else if (text.equals("(~pvr)^q") || text.equals("((rv~p)^q") || text.equals("q^(~pvr)") || text.equals("q^(rv~p)")){
	        	   a = false;
	                System.out.println("p\tq\tr\t~p\t~pvr\t" + eq.getText());
	                output.setText("p\tq\tr\t~p\t~pvr\t" + eq.getText());
	                do {
	                    b = false;
	                    do {
	                        c = false;
	                        do {
	                            System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a || c) + "\t" + ((!a || c) && b));
	                            output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!a || c) + "\t" + ((!a || c) && b));
	                            c = !c;
	                        }while(c);
	                        b = !b;
	                    }while(b);
	                    a =!a;
	                }while(a);
	           }

		       
		       //3 (p or not r) and q
		       else if (text.equals("(pv~r)^q") || text.equals("(~rvp)^q") || text.equals("q^(pv~r)") || text.equals("q^(~rvp)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\tpv~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\tpv~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a && !c) + "\t" + ((a || !c) && b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a || !c) + "\t" + ((a || !c) && b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p or not r) and q
		       else if (text.equals("(~pv~r)^q") || text.equals("(~rv~p)^q") || text.equals("q^(~pv~r)") || text.equals("q^(~rv~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~r\t~pv~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~r\t~pv~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a || !c) + "\t" + ((!a || !c) && b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (!a || !c) + "\t" + ((!a || !c) && b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (p or r) and not q
		       else if (text.equals("(pvr)^~q") || text.equals("(rvp)^~q") || text.equals("~q^(pvr)") || text.equals("~q^(rvp)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\tpvr\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\tpvr\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a || c) + "\t" + ((a || c) && !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a || c) + "\t" + ((a || c) && !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p or r) and not q
		       else if (text.equals("(~pvr)^~q") || text.equals("(rv~p)^~q") || text.equals("~q^(~pvr)") || text.equals("~q^(rv~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q\t~pvr\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q\t~pvr\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a || c) + "\t" + ((!a || c) && !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!a || c) + "\t" + ((!a || c) && !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (p or not r) and not q
		       else if (text.equals("(pv~r)^~q") || text.equals("(~rvp)^~q") || text.equals("~q^(pv~r)") || text.equals("~q^(~rvp)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\t~r\tpv~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\t~r\tpv~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a || !c) + "\t" + ((a || !c) && !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (a || !c) + "\t" + ((a || !c) && !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p or not r) and not q
		       else if (text.equals("(~pv~r)^~q") || text.equals("(~rv~p)^~q") || text.equals("~q^(~pv~r)") || text.equals("~q^(~rv~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q\t~r\t~pv~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q\t~r\t~pv~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!a || !c) + "\t" + ((!a || !c) && !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t"  + !c + "\t" + (!a || !c) + "\t" + ((!a || !c) && !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       
		       //3 (q or r) and p
		       else if (text.equals("(rvq)^p") || text.equals("(qvr)^p") || text.equals("p^(rvq)") || text.equals("p^(qvr)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tqvr\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tqvr\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (b || c) + "\t" + ((b || c) && a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (b || c) + "\t" + ((b || c) && a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not q or r) and p
		       else if (text.equals("(rv~q)^p") || text.equals("(~qvr)^p") || text.equals("p^(rv~q)") || text.equals("p^(~qvr)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\t~qvr\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\t~qvr\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!b || c) + "\t" + ((!b || c) && a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!b || c) + "\t" + ((!b || c) && a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(q or not r) and p
		       else if (text.equals("(~rvq)^p") || text.equals("(qv~r)^p") || text.equals("p^(~rvq)") || text.equals("p^(qv~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\tqv~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\tqv~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (b || !c) + "\t" + ((b || !c) && a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (b || !c) + "\t" + ((b || !c) && a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not q or not r) and p
		       else if (text.equals("(~rv~q)^p") || text.equals("(~qv~r)^p") || text.equals("p^(~rv~q)") || text.equals("p^(~qv~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\t~r\t~qv~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\t~r\t~qv~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (!b || !c) + "\t" + ((!b || !c) && a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + !c + "\t" + (!b || !c) + "\t" + ((!b || !c) && a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (q or r) and not p
		       else if (text.equals("(rvq)^~p") || text.equals("(qvr)^~p") || text.equals("~p^(rvq)") || text.equals("~p^(qvr)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\tqvr\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\tqvr\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (b || c) + "\t" + ((b || c) && !a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (b || c) + "\t" + ((b || c) && !a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (q or not r) and not p
		       else if (text.equals("(~rvq)^~p") || text.equals("(qv~r)^~p") || text.equals("~p^(~rvq)") || text.equals("~p^(qv~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~r\tqv~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~r\tqv~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (b || !c) + "\t" + ((b || !c) && !a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !c + "\t" + (b || !c) + "\t" + ((b || !c) && !a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not q or r) and not p
		       else if (text.equals("(rv~q)^~p") || text.equals("(~qvr)^~p") || text.equals("~p^(rv~q)") || text.equals("~p^(~qvr)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q\t~qvr\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q\t~qvr\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!b || c) + "\t" + ((!b || c) && !a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + (!b || c) + "\t" + ((!b || c) && !a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not q or not r) and not p
		       else if (text.equals("(~rv~q)^~p") || text.equals("(~qv~r)^~p") || text.equals("~p^(~rv~q)") || text.equals("~p^(~qv~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q\t~r\t~qv~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q\t~r\t~qvr\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!b || !c) + "\t" + ((!b || !c) && !a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + !b + "\t" + !c + "\t" + (!b || !c) + "\t" + ((!b || !c) && !a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       
		       //3 (p implies q) OR r
		       else if (text.equals("(p->q)vr") || text.equals("rv(p->q)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tp->q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tp->q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!a || b) + "\t" + ((!a || b) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!a || b) + "\t" + ((!a || b) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p implies q) or r
		       else if (text.equals("(~p->q)vr") || text.equals("rv(~p->q)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p->q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p->q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (a || b) + "\t" + ((a || b) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (a || b) + "\t" + ((a || b) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (p implies not q) or r
		       else if (text.equals("(p->~q)vr") || text.equals("rv(p->~q)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tp->~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tp->~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!a || !b) + "\t" + ((!a || !b) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!a || !b) + "\t" + ((!a || !b) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (not p implies not q) or r
		       else if (text.equals("(~p->~q)vr") || text.equals("rv(~p->~q)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p->~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p->~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (a || !b) + "\t" + ((a || !b) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (a || !b) + "\t" + ((a || !b) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(p implies q) or not r
		       else if (text.equals("(p->q)v~r") || text.equals("~rv(p->q)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\tp->q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\tp->q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c+ "\t" + (!a || b) + "\t" + ((!a || b) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (!a || b) + "\t" + ((!a || b) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(not p implies q) or not r
		       else if (text.equals("(~p->q)v~r") || text.equals("~rv(~p->q)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\t~p->q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\t~p->q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c+ "\t" + (a || b) + "\t" + ((a || b) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a || b) + "\t" + ((a || b) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(p implies not q) or not r
		       else if (text.equals("(p->~q)v~r") || text.equals("~rv(p->~q)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\tp->~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\tp->~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c+ "\t" + (!a || !b) + "\t" + ((!a || !b) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (!a || !b) + "\t" + ((!a || !b) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3(not p implies not q) or not r
		       else if (text.equals("(~p->~q)v~r") || text.equals("~rv(~p->~q)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\t~p->~q\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\t~p->~q\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c+ "\t" + (a || !b) + "\t" + ((a || !b) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (a || !b) + "\t" + ((a || !b) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //3 (q implies p) or r
		       else if (text.equals("(q->p)vr") || text.equals("rv(q->p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tq->p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tq->p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!b || a) + "\t" + ((!b || a) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!b || a) + "\t" + ((!b || a) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not q imp p) or r
		       else if (text.equals("(~q->p)vr") || text.equals("rv(~q->p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q->p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q->p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (b || a) + "\t" + ((b || a) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (b || a) + "\t" + ((b || a) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(q imp not p) or r
		       else if (text.equals("(q->~p)vr") || text.equals("rv(q->~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tq->~p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tq->~p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!b || !a) + "\t" + ((!b || !a) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!b || !a) + "\t" + ((!b || !a) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not q imp not p) or r
		       else if (text.equals("(~q->~p)vr") || text.equals("rv(~q->~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q->~p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q->~p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (b || !a) + "\t" + ((b || !a) || c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (b || !a) + "\t" + ((b || !a) || c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(q imp p) or not r
		       else if (text.equals("(q->p)v~r") || text.equals("~rv(q->p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\tq->p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\tq->p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (!b || a) + "\t" + ((!b || a) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (!b || a) + "\t" + ((!b || a) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not q imp p) or not r
		       else if (text.equals("(~q->p)v~r") || text.equals("~rv(~q->p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\t~q->p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\t~q->p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (b || a) + "\t" + ((b || a) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (b || a) + "\t" + ((b || a) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(q imp not p) or not r
		       else if (text.equals("(q->~p)v~r") || text.equals("~rv(q->~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\tq->~p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\tq->~p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (!b || !a) + "\t" + ((!b || !a) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (!b || !a) + "\t" + ((!b || !a) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not q imp not p) or not r
		       else if (text.equals("(~q->~p)v~r") || text.equals("~rv(~q->~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r\t~q->~p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r\t~q->~p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (b || !a) + "\t" + ((b || !a) || !c));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !c + "\t" + (b || !a) + "\t" + ((b || !a) || !c));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       
		       //(p imp r) or q
		       else if (text.equals("(p->r)vq") || text.equals("qv(p->r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tp->r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tp->r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!a || c) + "\t" + ((!a || c) || b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!a || c) + "\t" + ((!a || c) || b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not p imp r) or q
		       else if (text.equals("(~p->r)vq") || text.equals("qv(~p->r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p->r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p->r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (a || c) + "\t" + ((a || c) || b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (a || c) + "\t" + ((a || c) || b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(p imp not r) or q
		       else if (text.equals("(p->~r)vq") || text.equals("qv(p->~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tp->~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tp->~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!a || !c) + "\t" + ((!a || !c) || b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!a || !c) + "\t" + ((!a || !c) || b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not p imp not r) or q
		       else if (text.equals("(~p->~r)vq") || text.equals("qv(~p->~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p->~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p->~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (a || !c) + "\t" + ((a || !c) || b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (a || !c) + "\t" + ((a || !c) || b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(p imp r) or not q
		       else if (text.equals("(p->r)v~q") || text.equals("~qv(p->r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\tp->r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\tp->r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b+ "\t" + (!a || c) + "\t" + ((!a || c) || !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!a || c) + "\t" + ((!a || c) || !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not p imp r) or not q
		       else if (text.equals("(~p->r)v~q") || text.equals("~qv(~p->r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\t~p->r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\t~p->r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b+ "\t" + (a || c) + "\t" + ((a || c) || !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a || c) + "\t" + ((a || c) || !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(p imp not r) or not q
		       else if (text.equals("(p->~r)v~q") || text.equals("~qv(p->~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\tp->~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\tp->~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b+ "\t" + (!a || !c) + "\t" + ((!a || !c) || !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!a || !c) + "\t" + ((!a || !c) || !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not p imp not r) or not q
		       else if (text.equals("(~p->~r)v~q") || text.equals("~qv(~p->~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\t~p->~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\t~p->~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b+ "\t" + (a || !c) + "\t" + ((a || !c) || !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (a || !c) + "\t" + ((a || !c) || !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       
		       //(r imp p) or q
		       else if (text.equals("(r->p)vq") || text.equals("qv(r->p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tr->p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tr->p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!c || a) + "\t" + ((!c || a) || b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!c || a) + "\t" + ((!c || a) || b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not r imp p) or q
		       else if (text.equals("(~r->p)vq") || text.equals("qv(~r->p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r->p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r->p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (c || a) + "\t" + ((c || a) || b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (c || a) + "\t" + ((c || a) || b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(r imp not p) or q
		       else if (text.equals("(r->~p)vq") || text.equals("qv(r->~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tr->~p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tr->~p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!c || !a) + "\t" + ((!c || !a) || b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!c || !a) + "\t" + ((!c || !a) || b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not r imp not p) or q
		       else if (text.equals("(~r->~p)vq") || text.equals("qv(~r->~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~r->~p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~r->~p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (c || !a) + "\t" + ((c || !a) || b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (c || !a) + "\t" + ((c || !a) || b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(r imp p) or not q
		       else if (text.equals("(r->p)v~q") || text.equals("~qv(r->p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\tr->p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\tr->p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!c || a) + "\t" + ((!c || a) || !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!c || a) + "\t" + ((!c || a) || !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not r imp p) or not q
		       else if (text.equals("(~r->p)v~q") || text.equals("~qv(~r->p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\t~r->p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\t~r->p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (c || a) + "\t" + ((c || a) || !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (c || a) + "\t" + ((c || a) || !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(r imp not p) or not q
		       else if (text.equals("(r->~p)v~q") || text.equals("~qv(r->~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\tr->~p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\tr->~p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!c || !a) + "\t" + ((!c || !a) || !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (!c || !a) + "\t" + ((!c || !a) || !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not r imp not p) or not q
		       else if (text.equals("(~r->~p)v~q") || text.equals("~qv(~r->~p)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q\t~r->~p\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q\t~r->~p\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (c || !a) + "\t" + ((c || !a) || !b));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !b + "\t" + (c || !a) + "\t" + ((c || !a) || !b));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       
		       //(q imp r) or p
		       else if (text.equals("(q->r)vp") || text.equals("pv(q->r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tq->r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tq->r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!b || c) + "\t" + ((!b || c) || a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!b || c) + "\t" + ((!b || c) || a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not q imp r) or p
		       else if (text.equals("(~q->r)vp") || text.equals("pv(~q->r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q->r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q->r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (b || c) + "\t" + ((b || c) || a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (b || c) + "\t" + ((b || c) || a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(q imp not r) or p
		       else if (text.equals("(q->~r)vp") || text.equals("pv(q->~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\tq->~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\tq->~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (!b || !c) + "\t" + ((!b || !c) || a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (!b || !c) + "\t" + ((!b || !c) || a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not q imp not r) or p
		       else if (text.equals("(~q->~r)vp") || text.equals("pv(~q->~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~q->~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~q->~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + (b || !c) + "\t" + ((b || !c) || a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + (b || !c) + "\t" + ((b || !c) || a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(q imp r) or not p
		       else if (text.equals("(q->r)v~p") || text.equals("~pv(q->r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\tq->r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\tq->r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!b || c) + "\t" + ((!b || c) || !a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!b || c) + "\t" + ((!b || c) || !a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not q imp r) or not p
		       else if (text.equals("(~q->r)v~p") || text.equals("~pv(~q->r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q->r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q->r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (b || c) + "\t" + ((b || c) || !a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (b || c) + "\t" + ((b || c) || !a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(q imp not r) or not p
		       else if (text.equals("(q->~r)v~p") || text.equals("~pv(q->~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\tq->~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\tq->~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!b || !c) + "\t" + ((!b || !c) || !a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (!b || !c) + "\t" + ((!b || !c) || !a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       //(not q imp not r) or not p
		       else if (text.equals("(~q->~r)v~p") || text.equals("~pv(~q->~r)")){
	    	   		a = false;
	    	   		System.out.println("p\tq\tr\t~p\t~q->~r\t" + eq.getText());
	    	   		output.setText("p\tq\tr\t~p\t~q->~r\t" + eq.getText());
	    	   		do {
	    	   			b = false;
	    	   			do {
	    	   				c = false;
	    	   				do {
	    	   					System.out.println(a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (b || !c) + "\t" + ((b || !c) || !a));
	    	   					output.setText(output.getText() + "\n" + a + "\t" + b + "\t" + c + "\t" + !a + "\t" + (b || !c) + "\t" + ((b || !c) || !a));
	    	   					c = !c;
	    	   				}while(c);
	    	   				b = !b;
	    	   			}while(b);
	    	   			a =!a;
	    	   		}while(a);
	           }
		       
		       
		         
		       
		       //end of three variable cases
		       eq.setText(null);
	    	  
		        } //end of Enter Button
		    
			
			
			
			}//end of actionPerformed
		
		
		
		
	}//end of buttonListener
	
	
}//end of TablePanel 
