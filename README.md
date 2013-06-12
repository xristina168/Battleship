import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class Battleship extends JFrame implements ActionListener{
  private static final int length=10;
	private JPanel panel, nPanel, nwPanel, ncPanel, nePanel, sPanel, ePanel, wPanel, cPanel, swPanel, scPanel, sePanel;
	private JLabel lbl1, lbl2, lbl3, lbl15, lbl16, lbl17;
	private JTextArea ta, ta2;
	private JScrollPane sbrText, helpText; 
	private JButton b1, b2, b3, b4, b5, b7, b8, b9, b10, b11, b12, b13, b14, b15, b16, b17;
	private JMenuBar menuBar;
	private JMenu menu1, menu2, menu3;
	private JMenuItem newGame, abandonGame, endGame, player1Turn, player2Turn, showScore, help, about, exit;
	private JButton buttons2[][] = new JButton[length][length];
	private JButton buttons1[][] = new JButton[length][length];
	private int counter = 0, turn1Counter = 0, turn2Counter = 0, ship1Counter = 0, ship2Counter = 0, win1Counter = 0, win2Counter = 0;
	private boolean theseis1 = true, theseis = true, a = true, hit1 = true, hit2 = true;
	private String player1Name = "", player2Name = "", orientation; 
	private Game game;
	private JFrame f;
	
	public Battleship(){
		super("Battleship");
		JOptionPane.showMessageDialog(null, "Καλωσήρθατε στην Ναυμαχία");		
		player1Name = (String)JOptionPane.showInputDialog("Παίκτης 1: ", "Player1");
		player2Name = (String)JOptionPane.showInputDialog("Παίκτης 2: ", "Player2");			
		game = new Game(player1Name, player2Name);
		panel = new JPanel();
		panel.setLayout(new BorderLayout());	
		nPanel = new JPanel();
		nPanel.setLayout(new BorderLayout());		
		nwPanel = new JPanel();
		nwPanel.setLayout(new FlowLayout());
		ncPanel = new JPanel();
		ncPanel.setLayout(new FlowLayout());
		nePanel = new JPanel();
		nePanel.setLayout(new FlowLayout());
		sPanel = new JPanel();
		sPanel.setLayout(new BorderLayout());
		ePanel = new JPanel();
		ePanel.setLayout(new GridLayout(10,10));
		wPanel = new JPanel();
		wPanel.setLayout(new GridLayout(10,10));
		cPanel = new JPanel();		
		cPanel.setLayout(new BoxLayout(cPanel, BoxLayout.PAGE_AXIS));
		swPanel = new JPanel();		
		swPanel.setLayout(new BoxLayout(swPanel, BoxLayout.PAGE_AXIS));
		scPanel = new JPanel();
		scPanel.setLayout(new FlowLayout());
		sePanel = new JPanel();		
		sePanel.setLayout(new BoxLayout(sePanel, BoxLayout.PAGE_AXIS));
	
		Font f = new Font("Arial", Font.BOLD, 36);
		Font f1 = new Font("Arial", Font.BOLD, 24);		
		lbl1 = new JLabel("Battleship Game");
		lbl1.setFont(f);	
		lbl15 = new JLabel(game.getPlayer1().getName());
		lbl15.setFont(f1);
		lbl15.setForeground(Color.WHITE);
		lbl16 = new JLabel(game.getPlayer2().getName());
		lbl16.setFont(f1);
		lbl16.setForeground(Color.WHITE);
		
	
		
		
		ImageIcon icon6 = new ImageIcon("images/battleshiposter.jpg");
		lbl17 = new JLabel(icon6);	
		
		nwPanel.add(lbl15);
		ncPanel.add(lbl17);
		nePanel.add(lbl16);
		nwPanel.setBackground(Color.BLUE.darker().darker());
		ncPanel.setBackground(Color.BLUE.darker().darker());
		nePanel.setBackground(Color.BLUE.darker().darker());		
		
		ta = new JTextArea(7, 40);
		ta.setEditable(false);
		ta.setLineWrap(true);
		sbrText = new JScrollPane(ta);
		sbrText.setVerticalScrollBarPolicy(JScrollPane.VERTICAL_SCROLLBAR_ALWAYS);
		ImageIcon icon1 = new ImageIcon("images/carrier.gif");
		b7 = new JButton(icon1);
		b7.addActionListener(this);		
		b7.setEnabled(false);
		ImageIcon icon2 = new ImageIcon("images/battleship.gif");
		b8 = new JButton(icon2);
		b8.addActionListener(this);
		b8.setEnabled(false);
		ImageIcon icon3 = new ImageIcon("images/submarine.gif");
		b9 = new JButton(icon3);
		b9.addActionListener(this);
		b9.setEnabled(false);
		ImageIcon icon4 = new ImageIcon("images/cruiser.gif");
		b10 = new JButton(icon4);
		b10.addActionListener(this);
		b10.setEnabled(false);
		ImageIcon icon5 = new ImageIcon("images/destr.gif");
		b11 = new JButton(icon5);
		b11.addActionListener(this);
		b11.setEnabled(false);
		
		b12 = new JButton(icon1);
		b12.addActionListener(this);
		b12.setEnabled(false);
		b13 = new JButton(icon2);
		b13.addActionListener(this);
		b13.setEnabled(false);
		b14 = new JButton(icon3);
		b14.addActionListener(this);
		b14.setEnabled(false);
		b15 = new JButton(icon4);
		b15.addActionListener(this);
		b15.setEnabled(false);
		b16 = new JButton(icon5);
		b16.addActionListener(this);
		b16.setEnabled(false);
		
		swPanel.add(b7);
		swPanel.add(b8);
		swPanel.add(b9);
		swPanel.add(b10);
		swPanel.add(b11);	
		scPanel.add(sbrText);
		sePanel.add(b12);
		sePanel.add(b13);
		sePanel.add(b14);
		sePanel.add(b15);
		sePanel.add(b16);

		swPanel.setBackground(Color.BLUE.darker().darker());
		scPanel.setBackground(Color.BLUE.darker().darker());
		sePanel.setBackground(Color.BLUE.darker().darker());
				
		for(int i=0; i<length; i++){
			for(int j=0; j<length; j++){
			buttons2[i][j] = new JButton();	
			buttons2[i][j].setEnabled(false);
			buttons2[i][j].setBackground(Color.LIGHT_GRAY);	
			buttons2[i][j].addActionListener(this);
			ePanel.add(buttons2[i][j]);	
			}
		}		
		for(int i=0; i<length; i++){
			for(int j=0; j<length; j++){
			buttons1[i][j] = new JButton();
			buttons1[i][j].setEnabled(false);
			buttons1[i][j].setBackground(Color.LIGHT_GRAY);
			buttons1[i][j].addActionListener(this);
			wPanel.add(buttons1[i][j]);	
			}
		}	
				
		b1 = new JButton("Νέο Παιχνίδι");
		b1.addActionListener(this);
		b1.setAlignmentX(Component.CENTER_ALIGNMENT);
	
		b2 = new JButton("Σειρά του Παίκτη 1");
		b2.addActionListener(this);
		b2.setAlignmentX(Component.CENTER_ALIGNMENT);
		b2.setEnabled(false);
		
		b17 = new JButton("Σειρά του Παίκτη 2");
		b17.addActionListener(this);
		b17.setAlignmentX(Component.CENTER_ALIGNMENT);
		b17.setEnabled(false);
				
		b3 = new JButton("Εγκαταλείψτε το παιχνίδι");
		b3.addActionListener(this);
		b3.setAlignmentX(Component.CENTER_ALIGNMENT);
		b3.setEnabled(false);
		
		b4 = new JButton("Τέλος Παιχνιδιού");
		b4.addActionListener(this);
		b4.setAlignmentX(Component.CENTER_ALIGNMENT);
		b4.setEnabled(false);
		
		b5 = new JButton("Εμφάνιση Βαθμολογίας");
		b5.addActionListener(this);
		b5.setAlignmentX(Component.CENTER_ALIGNMENT);
		b5.setEnabled(false);
		
		lbl2 = new JLabel("Η βαθμολογία είναι: και ο νικητής είναι: ");
		lbl2.setVisible(false);
		lbl3 = new JLabel("Ο νικητής είναι: ");
		lbl3.setVisible(false);
		
		cPanel.add(b1);	
		cPanel.add(b2);
		cPanel.add(b17);
		cPanel.add(b3);
		cPanel.add(b4);
		cPanel.add(b5);		
		
		cPanel.add(lbl2);
		cPanel.add(lbl3);		
			
		cPanel.setBackground(Color.BLUE.darker().darker());		
		
		sPanel.add(swPanel, BorderLayout.WEST);
		sPanel.add(scPanel, BorderLayout.CENTER);
		sPanel.add(sePanel, BorderLayout.EAST);
		
		nPanel.add(nwPanel, BorderLayout.WEST);
		nPanel.add(ncPanel, BorderLayout.CENTER);
		nPanel.add(nePanel, BorderLayout.EAST);
		
		panel.add(nPanel, BorderLayout.NORTH);
		panel.add(sPanel, BorderLayout.SOUTH);
		panel.add(ePanel, BorderLayout.EAST);
		panel.add(wPanel, BorderLayout.WEST);
		panel.add(cPanel, BorderLayout.CENTER);
		MenuListener menulistener = new MenuListener();
		menu1 = new JMenu("Αρχείο");
		newGame = new JMenuItem("Νέο Παιχνίδι");
		newGame.addActionListener(menulistener);
		abandonGame = new JMenuItem("Εγκαταλείψτε");
		abandonGame.addActionListener(menulistener);
		endGame = new JMenuItem("Τέλος Παιχνιδιού");
		endGame.addActionListener(menulistener);
		menu1.add(newGame);
		menu1.add(abandonGame);
		menu1.add(endGame);
		menu2 = new JMenu("Επιλογές");
		player1Turn = new JMenuItem("Σειρά του Παίκτη 1");
		player2Turn = new JMenuItem("Σειρά του Παίκτη 2");
		showScore = new JMenuItem("Εμφάνιση Βαθμολογίας");
		menu2.add(player1Turn);
		menu2.add(player2Turn);
		menu2.add(showScore);
		menu3 = new JMenu("Βοήθεια");
		help = new JMenuItem("Βοήθεια");
		help.addActionListener(menulistener);
		about = new JMenuItem("Σχετικά");
		about.addActionListener(menulistener);
		exit = new JMenuItem("Έξοδος");
		exit.addActionListener(menulistener);
		menu3.add(help);
		menu3.add(about);
		menu3.add(exit);
		menuBar= new JMenuBar();
		menuBar.add(menu1);
		menuBar.add(menu2);
		menuBar.add(menu3);
		
		this.setJMenuBar(menuBar);
		this.setContentPane(panel);
		this.setSize(900, 900);
		this.setVisible(true);
		this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);			
	}
	
	public void actionPerformed(ActionEvent e) {
		
		if(e.getSource()==b1){			
			b3.setEnabled(true);
			b4.setEnabled(true);
			b5.setEnabled(true);
			b7.setEnabled(true);			
			if(counter==0){
				for(int i=0; i<length; i++){
					for(int j=0; j<length; j++){				
						buttons2[i][j].setEnabled(true);	
						buttons1[i][j].setEnabled(true);
						buttons2[i][j].setBackground(Color.BLUE.brighter().brighter());
						buttons1[i][j].setBackground(Color.BLUE.brighter().brighter());
					}
				}
					counter++;
				}else{
					for(int i=0; i<length; i++){
						for(int j=0; j<length; j++){				
							buttons2[i][j].setBackground(null);	
							buttons2[i][j].setEnabled(true);	
							buttons2[i][j].setSelected(false);
							buttons1[i][j].setBackground(null);	
							buttons1[i][j].setEnabled(true);	
							buttons1[i][j].setSelected(false);	
							buttons2[i][j].setBackground(Color.BLUE.brighter().brighter());
							buttons1[i][j].setBackground(Color.BLUE.brighter().brighter());
						}
					}
					counter++;
			}
			ta.append("Καλωσήρθατε στη Ναυμαχία"+"\n");
			ta.append("O " +game.getPlayer1().getName()+ " να τοποθετήσει τα πλοία του"+"\n");
		}
		if(e.getSource()==b3){
			int reply = JOptionPane.showConfirmDialog(null, "Είστε σίγουρος πως θέλετε να εγκαταλείψετε το παιχνίδι;", "Προειδοποίηση", JOptionPane.YES_NO_OPTION);
			if(reply == JOptionPane.YES_OPTION){
				for(int i=0; i<length; i++){
					for(int j=0; j<length; j++){					
					buttons2[i][j].setEnabled(false);
					buttons1[i][j].setEnabled(false);
					buttons2[i][j].setBackground(Color.LIGHT_GRAY);		
					buttons1[i][j].setBackground(Color.LIGHT_GRAY);	
					}
				}								
			}
		}
		if(e.getSource()==b4){
			int reply = JOptionPane.showConfirmDialog(null, "Είστε σίγουρος πως θέλετε να πραγματοποιήσετε έξοδο από το παιχνίδι;", "Προειδοποίηση", JOptionPane.YES_NO_OPTION);
			if(reply == JOptionPane.YES_OPTION){
			System.exit(0);
			}
		}
		
		if(e.getSource()==b5){	
			if(win1Counter==17){
				JOptionPane.showMessageDialog(null, "Ο νικητής είναι ο "+game.getPlayer1().getName());
			}else if(win2Counter==17){
				JOptionPane.showMessageDialog(null, "Ο νικητής είναι ο "+game.getPlayer2().getName());
			}else{
				JOptionPane.showMessageDialog(null, "Δεν υπάρχει νικητής");
			}
			
		}		
		if(e.getSource()==b7){	
			b7.setEnabled(false);
			b7.setSelected(true);
			b8.setEnabled(true);
			ta.append("Τοποθετήστε το AircraftCarrier"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");			
		}
		if(e.getSource()==b8){
			b8.setEnabled(false);
			b8.setSelected(true);
			b9.setEnabled(true);
			ta.append("Τοποθετήστε το Battleship"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");			
		}
		if(e.getSource()==b9){
			b9.setEnabled(false);
			b9.setSelected(true);
			b10.setEnabled(true);
			ta.append("Τοποθετήστε το Submarine"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");			
		}
		if(e.getSource()==b10){
			b10.setEnabled(false);
			b10.setSelected(true);
			b11.setEnabled(true);
			ta.append("Τοποθετήστε το Cruiser"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
		}
		if(e.getSource()==b11){
			b11.setEnabled(false);
			b11.setSelected(true);
			ta.append("Τοποθετήστε το Destroyer"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
			ta.append("O " +game.getPlayer2().getName()+ " να τοποθετήσει τα πλοία του"+"\n");			
		}
		if(e.getSource()==b12){	
			b12.setEnabled(false);
			b12.setSelected(true);
			b13.setEnabled(true);
			ta.append("Τοποθετήστε το AircraftCarrier"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
		}
		if(e.getSource()==b13){	
			b13.setEnabled(false);
			b13.setSelected(true);
			b14.setEnabled(true);
			ta.append("Τοποθετήστε το Battleship"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
		}
		if(e.getSource()==b14){
			b14.setEnabled(false);
			b14.setSelected(true);
			b15.setEnabled(true);
			ta.append("Τοποθετήστε το Submarine"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
		}
		if(e.getSource()==b15){
			b15.setEnabled(false);
			b15.setSelected(true);
			b16.setEnabled(true);
			ta.append("Τοποθετήστε το Cruiser"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
		}
		if(e.getSource()==b16){
			b16.setEnabled(false);
			b16.setSelected(true);
			ta.append("Τοποθετήστε το Destroyer"+"\n");
			orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
		}
		
		if(e.getSource()==b17){		
			hit2=true;
			a = false;
			if(turn1Counter==0){
				b12.setEnabled(false);
				b17.setEnabled(false);
				wPanel.setVisible(false);	
				b12.setEnabled(true);
				turn1Counter++;
			}else if(turn1Counter==1){
				b17.setEnabled(false);
				for(int i=0; i<length; i++){
					for(int j=0; j<length; j++){	
						if(buttons1[i][j].isEnabled()==true){
						buttons1[i][j].setBackground(Color.BLUE.brighter().brighter());
						}
						}						
					}
				for(int i=0; i<length; i++){
					for(int j=0; j<length; j++){
						if(buttons2[i][j].isSelected()==true){
							if(buttons1[i][j].isEnabled()==true){
							buttons2[i][j].setBackground(Color.LIGHT_GRAY);
							}
							}							
						}						
					}
				wPanel.setVisible(true);
				ePanel.setVisible(true);
			}else{
				b17.setEnabled(false);
				for(int i=0; i<length; i++){
					for(int j=0; j<length; j++){	
						if(buttons1[i][j].isEnabled()==true){
						buttons1[i][j].setBackground(Color.BLUE.brighter().brighter());
						}
						}
				}
				for(int i=0; i<length; i++){
					for(int j=0; j<length; j++){
						if(buttons2[i][j].isSelected()==true){
							if(buttons1[i][j].isEnabled()==true){
							buttons2[i][j].setBackground(Color.LIGHT_GRAY);
							}
							}							
						}						
					}					
			}
	}
	
	if(e.getSource()==b2){
		hit1=true;
		a = true;
		if(turn2Counter==0){
			b12.setEnabled(false);
			b2.setEnabled(false);				
			b12.setEnabled(true);
			turn2Counter++;
			for(int i=0; i<length; i++){
				for(int j=0; j<length; j++){	
					if(buttons2[i][j].isEnabled()==true){
					buttons2[i][j].setBackground(Color.BLUE.brighter().brighter());
					}		
				}
				}
			ePanel.setVisible(true);
			wPanel.setVisible(true);
			b17.setEnabled(true);
		}else{
			b2.setEnabled(false);
			for(int i=0; i<length; i++){
				for(int j=0; j<length; j++){	
					if(buttons2[i][j].isEnabled()==true){
					buttons2[i][j].setBackground(Color.BLUE.brighter().brighter());
					}
				}
			}
			for(int i=0; i<length; i++){
				for(int j=0; j<length; j++){
					if(buttons1[i][j].isSelected()==true){
						if(buttons2[i][j].isEnabled()==true){
						buttons1[i][j].setBackground(Color.LIGHT_GRAY);
						}
					}
					}						
				}	
			ePanel.setVisible(true);
			wPanel.setVisible(true);
		}
		
			
			
	}	
	
		for(int i=0; i<length; i++){
			for(int j=0; j<length; j++){				
				if(e.getSource()==buttons1[i][j]){
					if(b7.isSelected()==true&&b8.isSelected()==false&&b9.isSelected()==false&&b10.isSelected()==false&&b11.isSelected()==false){
						if(orientation.equals("1")){
							if(theseis1){
								buttons1[i][j].setSelected(true);
								buttons1[i][j+1].setSelected(true);
								buttons1[i][j+2].setSelected(true);
								buttons1[i][j+3].setSelected(true);
								buttons1[i][j+4].setSelected(true);								
								buttons1[i][j].setBackground(Color.LIGHT_GRAY);
								buttons1[i][j+1].setBackground(Color.LIGHT_GRAY);
								buttons1[i][j+2].setBackground(Color.LIGHT_GRAY);
								buttons1[i][j+3].setBackground(Color.LIGHT_GRAY);
								buttons1[i][j+4].setBackground(Color.LIGHT_GRAY);
								theseis1 = false;
							}else{
								JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
							}
						}else if(orientation.equals("2")){
							if(theseis1){
								buttons1[i][j].setSelected(true);
								buttons1[i+1][j].setSelected(true);
								buttons1[i+2][j].setSelected(true);
								buttons1[i+3][j].setSelected(true);
								buttons1[i+4][j].setSelected(true);														
								buttons1[i][j].setBackground(Color.LIGHT_GRAY);
								buttons1[i+1][j].setBackground(Color.LIGHT_GRAY);
								buttons1[i+2][j].setBackground(Color.LIGHT_GRAY);
								buttons1[i+3][j].setBackground(Color.LIGHT_GRAY);
								buttons1[i+4][j].setBackground(Color.LIGHT_GRAY);
								theseis1 = false;
							}else{
								JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}
					}else if(b7.isSelected()==true&&b8.isSelected()==true&&b9.isSelected()==false&&b10.isSelected()==false&&b11.isSelected()==false){
						if(orientation.equals("1")){
							if(buttons1[i][j].isSelected()==true||buttons1[i][j+1].isSelected()==true||buttons1[i][j+2].isSelected()==true||buttons1[i][j+3].isSelected()==true){
								JOptionPane.showMessageDialog(null, "I thesi einai kateleimmeni");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(!theseis1){
									buttons1[i][j].setSelected(true);
									buttons1[i][j+1].setSelected(true);
									buttons1[i][j+2].setSelected(true);
									buttons1[i][j+3].setSelected(true);
									buttons1[i][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i][j+1].setBackground(Color.LIGHT_GRAY);
									buttons1[i][j+2].setBackground(Color.LIGHT_GRAY);
									buttons1[i][j+3].setBackground(Color.LIGHT_GRAY);
									theseis1 = true;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}							
						}else if(orientation.equals("2")){
							if(buttons1[i][j].isSelected()==true||buttons1[i+1][j].isSelected()==true||buttons1[i+2][j].isSelected()==true||buttons1[i+3][j].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");
							}else{
								if(!theseis1){
									buttons1[i][j].setSelected(true);
									buttons1[i+1][j].setSelected(true);
									buttons1[i+2][j].setSelected(true);
									buttons1[i+3][j].setSelected(true);
									buttons1[i][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i+1][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i+2][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i+3][j].setBackground(Color.LIGHT_GRAY);	
									theseis1 = true;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}
					}else if(b7.isSelected()==true&&b8.isSelected()==true&&b9.isSelected()==true&&b10.isSelected()==false&&b11.isSelected()==false){
						if(orientation.equals("1")){
							if(buttons1[i][j].isSelected()==true||buttons1[i][j+1].isSelected()==true||buttons1[i][j+2].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(theseis1){
									buttons1[i][j].setSelected(true);
									buttons1[i][j+1].setSelected(true);
									buttons1[i][j+2].setSelected(true);
									buttons1[i][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i][j+1].setBackground(Color.LIGHT_GRAY);
									buttons1[i][j+2].setBackground(Color.LIGHT_GRAY);	
									theseis1 = false;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else if(orientation.equals("2")){
							if(buttons1[i][j].isSelected()==true||buttons1[i+1][j].isSelected()==true||buttons1[i+2][j].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(theseis1){
									buttons1[i][j].setSelected(true);
									buttons1[i+1][j].setSelected(true);
									buttons1[i+2][j].setSelected(true);
									buttons1[i][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i+1][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i+2][j].setBackground(Color.LIGHT_GRAY);	
									theseis1 = false;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}						
					}else if(b7.isSelected()==true&&b8.isSelected()==true&&b9.isSelected()==true&&b10.isSelected()==true&&b11.isSelected()==false){
						if(orientation.equals("1")){
							if(buttons1[i][j].isSelected()==true||buttons1[i][j+1].isSelected()==true||buttons1[i][j+2].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(!theseis1){
									buttons1[i][j].setSelected(true);
									buttons1[i][j+1].setSelected(true);
									buttons1[i][j+2].setSelected(true);
									buttons1[i][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i][j+1].setBackground(Color.LIGHT_GRAY);
									buttons1[i][j+2].setBackground(Color.LIGHT_GRAY);	
									theseis1 = true;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else if(orientation.equals("2")){
							if(buttons1[i][j].isSelected()==true||buttons1[i+1][j].isSelected()==true||buttons1[i+2][j].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(!theseis1){
									buttons1[i][j].setSelected(true);
									buttons1[i+1][j].setSelected(true);
									buttons1[i+2][j].setSelected(true);
									buttons1[i][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i+1][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i+2][j].setBackground(Color.LIGHT_GRAY);		
									theseis1 = true;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}
					}else if(b7.isSelected()==true&&b8.isSelected()==true&&b9.isSelected()==true&&b10.isSelected()==true&&b11.isSelected()==true){
						if(ship1Counter==0){
							ship1Counter++;
						if(orientation.equals("1")){
							if(buttons1[i][j].isSelected()==true||buttons1[i][j+1].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(theseis1){
									buttons1[i][j].setSelected(true);
									buttons1[i][j+1].setSelected(true);
									buttons1[i][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i][j+1].setBackground(Color.LIGHT_GRAY);
									theseis1 = false;					
									b17.setEnabled(true);
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else if(orientation.equals("2")){
							if(buttons1[i][j].isSelected()==true||buttons1[i+1][j].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(theseis1){
									buttons1[i][j].setSelected(true);
									buttons1[i+1][j].setSelected(true);
									buttons1[i][j].setBackground(Color.LIGHT_GRAY);
									buttons1[i+1][j].setBackground(Color.LIGHT_GRAY);	
									theseis1 = false;
									b17.setEnabled(true);
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}
						}else{							
							if(!a){
								if(hit1==true){
							if(buttons1[i][j].isSelected()==true){
								buttons1[i][j].setBackground(Color.GREEN);
								buttons1[i][j].setEnabled(false);
								win1Counter++;
								if(win1Counter==17){
									JOptionPane.showMessageDialog(null, "Ο νικητής είναι ο "+game.getPlayer1().getName());
									ta.append("Ο " +game.getPlayer1().getName()+ " είναι ο νικητής"+"\n");
								}
								b2.setEnabled(true);
								ta.append("O " +game.getPlayer2().getName()+ " χτύπησε πλοίο"+"\n");
							}else{
								buttons1[i][j].setBackground(Color.RED);
								buttons1[i][j].setEnabled(false);
								b2.setEnabled(true);
								ta.append("O " +game.getPlayer2().getName()+ " απέτυχε"+"\n");
							}
							hit1=false;
							}else{
								JOptionPane.showMessageDialog(null, "Δεν μπορείτε να χτυπήσετε δυο φορές");
							}
						}else{
							JOptionPane.showMessageDialog(null, "Δεν μπορείτε να χτυπήσετε το δικό σας ταμπλό");
						}
						}
					}
				}
			}
	}

		for(int i=0; i<length; i++){
			for(int j=0; j<length; j++){				
				if(e.getSource()==buttons2[i][j]){
					if(b12.isSelected()==true&&b13.isSelected()==false&&b14.isSelected()==false&&b15.isSelected()==false&&b16.isSelected()==false){
						if(orientation.equals("1")){
							if(theseis){
								buttons2[i][j].setSelected(true);
								buttons2[i][j+1].setSelected(true);
								buttons2[i][j+2].setSelected(true);
								buttons2[i][j+3].setSelected(true);
								buttons2[i][j+4].setSelected(true);
								buttons2[i][j].setBackground(Color.LIGHT_GRAY);
								buttons2[i][j+1].setBackground(Color.LIGHT_GRAY);
								buttons2[i][j+2].setBackground(Color.LIGHT_GRAY);
								buttons2[i][j+3].setBackground(Color.LIGHT_GRAY);
								buttons2[i][j+4].setBackground(Color.LIGHT_GRAY);
								theseis = false;
							}else{
								JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
							}
						}else if(orientation.equals("2")){
							if(theseis){
								buttons2[i][j].setSelected(true);
								buttons2[i+1][j].setSelected(true);
								buttons2[i+2][j].setSelected(true);
								buttons2[i+3][j].setSelected(true);
								buttons2[i+4][j].setSelected(true);
								buttons2[i][j].setBackground(Color.LIGHT_GRAY);
								buttons2[i+1][j].setBackground(Color.LIGHT_GRAY);
								buttons2[i+2][j].setBackground(Color.LIGHT_GRAY);
								buttons2[i+3][j].setBackground(Color.LIGHT_GRAY);
								buttons2[i+4][j].setBackground(Color.LIGHT_GRAY);
								theseis = false;
							}else{
								JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}
					}else if(b12.isSelected()==true&&b13.isSelected()==true&&b14.isSelected()==false&&b15.isSelected()==false&&b16.isSelected()==false){
						if(orientation.equals("1")){
							if(buttons2[i][j].isSelected()==true||buttons2[i][j+1].isSelected()==true||buttons2[i][j+2].isSelected()==true||buttons2[i][j+3].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(!theseis){
									buttons2[i][j].setSelected(true);
									buttons2[i][j+1].setSelected(true);
									buttons2[i][j+2].setSelected(true);
									buttons2[i][j+3].setSelected(true);
									buttons2[i][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i][j+1].setBackground(Color.LIGHT_GRAY);
									buttons2[i][j+2].setBackground(Color.LIGHT_GRAY);
									buttons2[i][j+3].setBackground(Color.LIGHT_GRAY);
									theseis = true;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}							
						}else if(orientation.equals("2")){
							if(buttons2[i][j].isSelected()==true||buttons2[i+1][j].isSelected()==true||buttons2[i+2][j].isSelected()==true||buttons2[i+3][j].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");
							}else{
								if(!theseis){
									buttons2[i][j].setSelected(true);
									buttons2[i+1][j].setSelected(true);
									buttons2[i+2][j].setSelected(true);
									buttons2[i+3][j].setSelected(true);
									buttons2[i][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i+1][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i+2][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i+3][j].setBackground(Color.LIGHT_GRAY);	
									theseis = true;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}
					}else if(b12.isSelected()==true&&b13.isSelected()==true&&b14.isSelected()==true&&b15.isSelected()==false&&b16.isSelected()==false){
						if(orientation.equals("1")){
							if(buttons2[i][j].isSelected()==true||buttons2[i][j+1].isSelected()==true||buttons2[i][j+2].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(theseis){
									buttons2[i][j].setSelected(true);
									buttons2[i][j+1].setSelected(true);
									buttons2[i][j+2].setSelected(true);
									buttons2[i][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i][j+1].setBackground(Color.LIGHT_GRAY);
									buttons2[i][j+2].setBackground(Color.LIGHT_GRAY);	
									theseis = false;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else if(orientation.equals("2")){
							if(buttons2[i][j].isSelected()==true||buttons2[i+1][j].isSelected()==true||buttons2[i+2][j].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(theseis){
									buttons2[i][j].setSelected(true);
									buttons2[i+1][j].setSelected(true);
									buttons2[i+2][j].setSelected(true);
									buttons2[i][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i+1][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i+2][j].setBackground(Color.LIGHT_GRAY);	
									theseis = false;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}						
					}else if(b12.isSelected()==true&&b13.isSelected()==true&&b14.isSelected()==true&&b15.isSelected()==true&&b16.isSelected()==false){
						if(orientation.equals("1")){
							if(buttons2[i][j].isSelected()==true||buttons2[i][j+1].isSelected()==true||buttons2[i][j+2].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(!theseis){
									buttons2[i][j].setSelected(true);
									buttons2[i][j+1].setSelected(true);
									buttons2[i][j+2].setSelected(true);
									buttons2[i][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i][j+1].setBackground(Color.LIGHT_GRAY);
									buttons2[i][j+2].setBackground(Color.LIGHT_GRAY);	
									theseis = true;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else if(orientation.equals("2")){
							if(buttons2[i][j].isSelected()==true||buttons2[i+1][j].isSelected()==true||buttons2[i+2][j].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(!theseis){
									buttons2[i][j].setSelected(true);
									buttons2[i+1][j].setSelected(true);
									buttons2[i+2][j].setSelected(true);
									buttons2[i][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i+1][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i+2][j].setBackground(Color.LIGHT_GRAY);		
									theseis = true;
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}
					}else if(b12.isSelected()==true&&b13.isSelected()==true&&b14.isSelected()==true&&b15.isSelected()==true&&b16.isSelected()==true){
						if(ship2Counter==0){
							ship2Counter++;
						if(orientation.equals("1")){
							if(buttons2[i][j].isSelected()==true||buttons2[i][j+1].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(theseis){
									buttons2[i][j].setSelected(true);
									buttons2[i][j+1].setSelected(true);
									buttons2[i][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i][j+1].setBackground(Color.LIGHT_GRAY);
									theseis = false;
									b2.setEnabled(true);
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else if(orientation.equals("2")){
							if(buttons2[i][j].isSelected()==true||buttons2[i+1][j].isSelected()==true){
								JOptionPane.showMessageDialog(null, "Η θέση είναι κατειλημμένη");
								orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
							}else{
								if(theseis){
									buttons2[i][j].setSelected(true);
									buttons2[i+1][j].setSelected(true);
									buttons2[i][j].setBackground(Color.LIGHT_GRAY);
									buttons2[i+1][j].setBackground(Color.LIGHT_GRAY);
									theseis = false;
									b2.setEnabled(true);
								}else{
									JOptionPane.showMessageDialog(null, "Το πλοίο έχει ήδη τοποθετηθεί");
								}
							}
						}else{
							JOptionPane.showMessageDialog(null, "Κάνατε λάθος καταχώριση");
							orientation = (String)JOptionPane.showInputDialog("Για οριζόντιο προσανατολισμό πιέστε 1 και για κάθετο προσανατολισμό 2");	
						}
					}else{
						if(a){
							if(hit2==true){
						if(buttons2[i][j].isSelected()==true){
							buttons2[i][j].setBackground(Color.GREEN);
							buttons2[i][j].setEnabled(false);
							win2Counter++;
							if(win2Counter==17){
								JOptionPane.showMessageDialog(null, "Ο νικητής είναι ο "+game.getPlayer2().getName());
								ta.append("O " +game.getPlayer2().getName()+ " είναι ο νικητής"+"\n");
							}
							b17.setEnabled(true);
							ta.append("O " +game.getPlayer1().getName()+ " χτύπησε πλοίο"+"\n");
						}else{
							buttons2[i][j].setBackground(Color.RED);
							buttons2[i][j].setEnabled(false);
							b17.setEnabled(true);
							ta.append("O " +game.getPlayer1().getName()+ " απέτυχε"+"\n");
						}
						hit2=false;
						}else{
							JOptionPane.showMessageDialog(null, "Δεν μπορείτε να χτυπήσετε δυο φορές");
						}
					}else{
						JOptionPane.showMessageDialog(null, "Δεν μπορείτε να χτυπήσετε το δικό σας ταμπλό");
					}
					}
					}
				}
			}
	}
	
	}
	
	public Game getGame() {
		return game;
	}
	
	class MenuListener implements ActionListener{

		
		public void actionPerformed(ActionEvent e) {
			String command = e.getActionCommand();
			if(command.equals("Νέο παιχνίδι")){
				b3.setEnabled(true);
				b4.setEnabled(true);
				b5.setEnabled(true);
				b7.setEnabled(true);			
				if(counter==0){
					for(int i=0; i<length; i++){
						for(int j=0; j<length; j++){				
							buttons2[i][j].setEnabled(true);	
							buttons1[i][j].setEnabled(true);
							buttons2[i][j].setBackground(Color.BLUE.brighter().brighter());
							buttons1[i][j].setBackground(Color.BLUE.brighter().brighter());
						}
					}
						counter++;
					}else{
						for(int i=0; i<length; i++){
							for(int j=0; j<length; j++){				
								buttons2[i][j].setBackground(null);	
								buttons2[i][j].setEnabled(true);	
								buttons2[i][j].setSelected(false);
								buttons1[i][j].setBackground(null);	
								buttons1[i][j].setEnabled(true);	
								buttons1[i][j].setSelected(false);	
								buttons2[i][j].setBackground(Color.BLUE.brighter().brighter());
								buttons1[i][j].setBackground(Color.BLUE.brighter().brighter());
							}
						}
						counter++;
				}
				ta.append("Καλωσήρθατε στη Ναυμαχία "+"\n");
				ta.append("O " +game.getPlayer1().getName()+ " να τοποθετήσει τα πλοία του"+"\n");
			}
		if(command.equals("Εγκαταλείψτε")){
			int reply = JOptionPane.showConfirmDialog(null, "Είστε σίγουρος πως θέλετε να εγκαταλείψετε το παιχνίδι;", "Προειδοποίηση", JOptionPane.YES_NO_OPTION);
			if(reply == JOptionPane.YES_OPTION){
				for(int i=0; i<length; i++){
					for(int j=0; j<length; j++){					
					buttons2[i][j].setEnabled(false);
					buttons1[i][j].setEnabled(false);
					buttons2[i][j].setBackground(Color.LIGHT_GRAY);		
					buttons1[i][j].setBackground(Color.LIGHT_GRAY);	
					}
					}								
				}
			}
		if(command.equals("Τέλος Παιχνιδιού")){
			int reply = JOptionPane.showConfirmDialog(null, "Είστε σίγουρος πως θέλετε να πραγματοποιήσετε έξοδο από το παιχνίδι;", "Προειδοποίηση", JOptionPane.YES_NO_OPTION);
			if(reply == JOptionPane.YES_OPTION){
			System.exit(0);
			}
		}
		if(command.equals("Έξοδος")){
			System.exit(0);
		}
		if(command.equals("Σχετικά")){
			JOptionPane.showMessageDialog(null, "Ναυμαχία "+"\n"+"Version: 1.0"+"\n"+"Ομάδα 8");
		}
		if(command.equals("Βοήθεια")){	
			f = new JFrame("Βοήθεια");
			Font font = new Font("Times New Roman", Font.PLAIN, 16);
			ta2 = new JTextArea();
			ta2.setText("Παπαδοπούλου, Πετρωτού, Χαραλαμπίδου");
			ta2.setEditable(false);
			ta2.setFont(font);
			helpText = new JScrollPane(ta2);
			helpText.setVerticalScrollBarPolicy(JScrollPane.VERTICAL_SCROLLBAR_ALWAYS);
			helpText.setHorizontalScrollBarPolicy(JScrollPane.HORIZONTAL_SCROLLBAR_ALWAYS);
			f.add(helpText);
			f.setVisible(true);
			f.setSize(400, 400);
		}
		}
		
		
	}
	
}
