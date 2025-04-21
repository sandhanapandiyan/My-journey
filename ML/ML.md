First Project:
  life cycle for devolepment MachineLearnning Model
  * Choose a best model for our Task
Source :
     Hugging face (Opesource plateform )
      https://huggingface.co/

  * Create a dataset for this to train (Collection of datas must in Json or Csv )
    example json for Text 2 sql trainning
     {
        "prompt": "Update location of department Target to Joshuafurt.",
        "query": "UPDATE department SET location = 'Joshuafurt' WHERE dept_name = 'Target';",
        "schema": "\nCREATE TABLE department (\n    dept_id INTEGER NOT NULL,\n    dept_name CHARACTER VARYING NOT NULL,\n    location CHARACTER VARYING NOT NULL,\n    head CHARACTER VARYING\n);\n\nCREATE TABLE employee (\n           emp_id INTEGER NOT NULL,\n    dept_id INTEGER,\n    salary NUMERIC,\n    hire_date DATE NOT NULL,\n    first_name CHARACTER VARYING NOT NULL,\n    last_name CHARACTER VARYING NOT NULL,\n    FOREIGN KEY (dept_id) 
         REFERENCES department(dept_id)\n);\n"
      },
 * Choose a Trainer To train the model
    pip install transformers (Architecture to support thr trainers )
       Trainers:
           Peft-Qlora
              (4 bit quandilization ue Bitssndbytes for this)
            Peft only save the Weights only to the Repo
            Merger the weights with model (Recomended)
   
from transformers import AutoTokenizer, AutoModelForCausalLM, BitsAndBytesConfig
import torch  #Above 2 lines Helps to import all the required librarys


model_id = "Sandhanapandiyan/model"   #model adapters on Hugging face

#Use to configuring Bitsand bytes for 4 bit quandilization
bnb_config = BitsAndBytesConfig(
    load_in_4bit=True,
    bnb_4bit_quant_type="nf4",
    bnb_4bit_compute_dtype=torch.float16,
    bnb_4bit_use_double_quant=True
)
   
    
