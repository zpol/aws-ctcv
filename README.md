# aws-ctcv
AWS ControlTower Security Controls Verifier




# Usage

Usage: ./aws-ctcv.sh <security_control_rule>
Example: ./aws-ctcv.sh WAF.6
	   ./aws-ctcv.sh -f <filename>
	   ./aws-ctcv.sh -r 
       ./aws-ctcv.sh -all


# Context

Sometimes when you are managing large AWS accounts with several hundreds of accounts hanging from the root account you may need to control what security control rules you
enable in ControlTower and also what SCP's and in what regions do you allow certain operations. From an organizanizational point of view managing so many accounts start to become a PITA when
there are multiple accounts and some technical debt.
Since AWS still do not allow to select a region to enable a security control rule ( it has to be all or nothing ). 
And since there are about 400 rules ( GuardDutty rules or Security Controls ), I came with the idea of scrapping the latest updated documentation I found on the AWS official website and check in a semi-automated way. 

https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-regions.html#securityhub-regions-control-support


# Description

This script helps you to extract ALL the AWS regions that DO NOT SUPPORT the security rule you're checking to enable in ControlTower. 
Basically extracts all the security controls list and availability per AWS region and check if the AWS Control Tower Security Control that you're checking is 
available or not in that region and it compares it with the REGIONS_ARRAY. 
This way it can help you to filter the almost 400 ruiles that AWS have in all the security frameworks right now and let you apply the ones that you're sure that
are not going to collide with your LandingZone and ControlTower regions configuration.

If you enter a security control and there's nothign shown by the script is probably an OK snd GO, but always double check! ;) 

# Configuration

The script was originally designed to only detect if a control rule id ( I.e: WAF.3 ) was in the controls not available on those regions.
But in order to ensure precision I decided to compare also those results with an array of regions in my environment, which basically ended up with this tool ( Still in development ) 

CONFIGURATION STEPS: 

1. Edit the REGIONS_ARRAY variable (inside `aws-ctcv.sh``) in order to make it compliance with your environment with the appropiate regions.
2. Make sure you have Internet connection ( not mandaroty as explained above )
3. `percol`is only required if `-r` flag is used. You can install it via `apt install -y percol`


# Requirements & dependencies
 It only requires Internet connection in order to retrieve the full security controls list and compare it with the local one, but since this function is disabled for now the script CAN WORK OFFLINE :) 
 ( That part is just commented , feeel free to play with it ) 
