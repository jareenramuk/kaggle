# kaggle
import pandas as pd

application_test=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/application_test.csv")
application_train=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/application_train.csv")
bureau=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/bureau.csv")
bureau_balance=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/bureau_balance.csv")
credit_card_balance=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/credit_card_balance.csv")
installments_payments=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/installments_payments.csv")
POS_CASH_balance=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/POS_CASH_balance.csv")
previous_application=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/previous_application.csv")
sample_submission=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/sample_submission.csv")

application_test1=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/application_test.csv",index_col="SK_ID_CURR")
application_train1=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/application_train.csv",index_col="SK_ID_CURR")
bureau1=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/bureau.csv",index_col="SK_ID_CURR")

credit_card_balance1=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/credit_card_balance.csv",index_col="SK_ID_CURR")
installments_payments1=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/installments_payments.csv",index_col="SK_ID_CURR")
POS_CASH_balance1=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/POS_CASH_balance.csv",index_col="SK_ID_CURR")
previous_application1=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/previous_application.csv",index_col="SK_ID_CURR")
sample_submission1=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/sample_submission.csv",index_col="SK_ID_CURR")

bureau_balance1=pd.read_csv("/Users/sneha_neeraj/Downloads/Kaggle_Home_Credit_20180811/bureau_balance.csv",index_col="SK_ID_BUREAU")

bureau_balance.sort_values(by=["SK_ID_BUREAU",'MONTHS_BALANCE'])

newDF = bureau_balance.drop_duplicates('SK_ID_BUREAU')
newDF['pattern']='_'

newDF2=pd.concat([pd.DataFrame([i], columns=['MONTHS_BALANCE']) for i in range(-96,1)],ignore_index=True)
newDF2['filler']='X'

k=0
for i in newDF1['SK_ID_BUREAU']:
    df1 = bureau_balance[bureau_balance['SK_ID_BUREAU']==i]
    newDF2['SK_ID_BUREAU']=i
    newDF3 = pd.merge(newDF2,df1,how='left',on=['SK_ID_BUREAU','MONTHS_BALANCE'])
    newDF3['STATUS'].fillna('X', inplace=True)
    newDF1['pattern'].iloc[k]=newDF3['STATUS'].str.cat(sep='')
    k=k+1
abc=pd.merge(bureau[['SK_ID_CURR','SK_ID_BUREAU']],application_train[['SK_ID_CURR','TARGET']], how = 'inner',
             on='SK_ID_CURR')
def1=pd.merge(abc,newDF1, how = 'inner',
             on='SK_ID_BUREAU')
