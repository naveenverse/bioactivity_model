# bioactivity_model
## Objective: 
To build a prediction model to understand the drug likeness property of a chemical molecule. 

## Approach: 
Druglikeness is a qualitative concept used in drug design for how "druglike" a substance is with respect to factors like bioavailability. It is estimated from the molecular structure before the substance is even synthesized and tested.
  ### Retreive bioactivity data:
      ! pip install chembl_webresource_client
      from chembl_webresource_client.new_client import new_client
First we retreive bioactivity of chemical data from ChEMBL database using chembl_webresource_client. We collect coumpounds with ChEMBL ID and its canonical SMILES and we label the groups 'active','intermediate','inactive' based on their bioactivity parametes.
  ### Calculate molecular descriptors
        ! conda install -c rdkit rdkit -y
        from rdkit import Chem
        from rdkit.Chem import Descriptors, Lipinski
We calculate Lipinski descriptors "MW","LogP","NumHDonors","NumHAcceptors" of the compouds based on SMILES.
Lipinski rule of 5 helps in distinguishing between drug like and non drug like molecules. It predicts high probability of success or failure due to drug likeness for molecules complying with 2 or more of the following rules.


Molecular mass less than 500 Dalton, High lipophilicity (expressed as LogP less than 5), Less than 5 hydrogen bond donors, Less than 10 hydrogen bond acceptors, Molar refractivity should be between 40-130.

We can also calculate molecular figerprints using PaDEL descriptors. We get 880 features describing a chemical compound.  
  ###
      ! bash padel.sh
  ### Model building
      from sklearn.ensemble import RandomForestRegressor
We build a regressor model and train it on 880 features obtained from padel descriptor calculation against bioactivity pIC50 as class label.
The model was able to perform with r2 value up to 0.54

  ### Visualization
<img width="263" alt="regplot" src="https://user-images.githubusercontent.com/59974158/137432869-a63b7d35-2965-48da-bc38-55a0c15fe5ed.png">
