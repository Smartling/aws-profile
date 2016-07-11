# aws-profile
Wrapper script to generate &amp; pass AWS AssumeRole keys to other scripts

- For now mfa_serial must be used to get this script working

- Requirements:
  boto3


AWSCLI configuration example.

- mfa_serial should be set to use MFA-Key


~/.aws/config

[profile assumed-role-profile1] 
output = json  
region = us-east-1   
role_arn = arn:aws:iam::XXXXXXXXXXXX:role/RoleAccountX   
source_profile =  source-profile   
mfa_serial = arn:aws:iam::XXXXXXXXXXX:mfa/virtual-mfa-device    

[profile assumed-role-profile2]    
output = json     
region = us-east-1     
role_arn = arn:aws:iam::YYYYYYYYYYYYYY:role/RoleAccountY    
source_profile =  source-profile    
mfa_serial = arn:aws:iam::XXXXXXXXXXX:mfa/virtual-mfa-device    


[profile source-profile]    
output = json    
region = us-east-1    


Without mfa_serial tries aws_profile to authenticate without MFA

Usage:
   
    aws-profile PROFILE COMMAND  

     -OR-

    In  aws-profile2  - rewrited arguments input, with possibility to integrate more features
    You have to put COMMAND between " " as example "comamnd p1 p2 p3 ...pN" to get it working

    aws-profile2 [-h] -p PROFILE -c COMMAND [-m MFA] [-s]

Wrapper script to generate & pass AWS AssumeRole keys to other scripts

optional arguments:   
  -h, --help            		show this help message and exit                  
  -p PROFILE, --profile PROFILE         Assume-Role profile                     
  -c COMMAND, --command COMMAND         Command to execute               
  -m MFA, --mfa MFA     		MFA token to authenticate            
  -s, --skipmfa         		Skip usage of MFA   
