# Java-Class-Project
import javafx.application.Application;
import javafx.event.ActionEvent;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.ChoiceBox;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.HBox;
import javafx.scene.layout.VBox;
import javafx.scene.text.Font;
import javafx.stage.Stage;

public class UniFees extends Application {
   
	  //INSTANCE VARIABLES
	  private ChoiceBox<String> choice1;
    private ChoiceBox<String> choice2;
    private Button calculate;

    //ARRAYS USED TO FILL CHOICE BOXES
    String[] dorms = {"No Dorm Selected","Allen Hall", "Smith Hall","William Hall","University Suites"};
    String[] mealPlans = {"No Meal Selected","7 meals per week", "14 meals per week","Unlimited meals"};
    
    //INTEGERS TO HOLD COSTS
    int dormFee;
    int mealFee;
    
    //TEXT FIELD TO DISPLAY CALCULATED COST
	  TextField field;
	  String displaytext = "Total Semester Charges";
    
    public void start(Stage primaryStage)
    {   
        //INITIALIZING TEXTFIELD AND LABEL
        field = new TextField(displaytext);	
        field.setFont(new Font(15)); 
        
        Label label = new Label("Select a dorm and meal plan:");
        
        //CREATING TWO CHOICE BOXES
        choice1 = new ChoiceBox<String>();
        choice1.getItems().addAll(dorms);
        choice1.getSelectionModel().selectFirst();
        choice1.setOnAction(this::processChoice1);
        
        choice2 = new ChoiceBox<String>();
        choice2.getItems().addAll(mealPlans);
        choice2.getSelectionModel().selectFirst();
        choice2.setOnAction(this::processChoice2);
        
        //CREATING TEXT CONTROL TO CALCULATE COST
        calculate = new Button("Calculate Cost");
        HBox button = new HBox(calculate);
        button.setSpacing(10);
        button.setPadding(new Insets(15, 0, 0, 0));
        button.setAlignment(Pos.CENTER);
        calculate.setOnAction(this::processButtonPush);
        
        //CREATING LAYOUT
        VBox root = new VBox(label, choice1,choice2,button, field);
        root.setPadding(new Insets(15, 15, 15, 25));
        root.setSpacing(10);
        root.setStyle("-fx-background-color: skyblue");
        
        Scene scene = new Scene(root, 300, 300);
        
        primaryStage.setTitle("University Living Expenses");
        primaryStage.setScene(scene);
        primaryStage.show();
    }
    
    //ACTIONEVENT FOR DORM CHOICE BOX
    public void processChoice1(ActionEvent event)
    {	
    	//STORE ARRAY INDEX OF CHOICE
    	int index = choice1.getSelectionModel().getSelectedIndex();
        
    	//USE INDEX TO DETERMINE COST AND STORE IN INTEGER
        switch(index) {
    		case 0:	dormFee = 0;	    //No Dorm selected
    				break;
        	case 1:	dormFee = 1800;	//Allen Hall
        			break;
        	case 2:	dormFee = 2000;	//Smith Hall
        			break;
        	case 3: dormFee = 2800;	//William Hall
        			break;
        	case 4:	dormFee = 3000;	//University Suites
        			break;
        }
        
     }
  
    //ACTIONEVENT FOR MEAL PLAN CHOICE BOX. FUNCTIONS LIKE PREVIOUS.
    public void processChoice2(ActionEvent event)
    {
    	int index = choice2.getSelectionModel().getSelectedIndex();
        
        switch(index) {
    		case 0:	mealFee = 0;	    //No Meal Selected
    				break;
        	case 1:	mealFee = 600;	//7 meals per week
        			break;
        	case 2:	mealFee = 1000;	//14 meals per week
        			break;
        	case 3: mealFee = 1800;	//Unlimited meals
        			break;
        }
        
     }

    //ACTIONEVENT FOR CALCULATE BUTTON
    public void processButtonPush(ActionEvent event)
    {	
    	//ADD COSTS AND STORE IN INTEGER. SET TEXTFIELD TO DISPLAY TOTAL COST. 
    	int cost = dormFee + mealFee;
    	field.setText("$" + Integer.toString(cost));
    }
    
    
    public static void main(String[] args)
    {
        launch(args);
    }
}
