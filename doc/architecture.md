# アーキテクチャ

本リポジトリのアーキテクチャを、UMLで記述します。

ここで記述しているアーキテクチャは、あくまで理想図です。



## OneCall Timer for Alexa

Alexaスキルによる OneCall Timer のアーキテクチャを、UMLの配置図で記述します。

```puml
@startuml
title OneCall Timer アーキテクチャ

!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v7.0/dist
!includeurl AWSPuml/AWSCommon.puml
' シンプルな枠組みに変更できる
' !includeurl AWSPuml/AWSSimplified.puml

!includeurl AWSPuml/InternetOfThings/IoTAlexaSkill.puml
!includeurl AWSPuml/Compute/Lambda.puml
!includeurl AWSPuml/Compute/LambdaLambdaFunction.puml
!includeurl AWSPuml/Database/DynamoDB.puml
!includeurl AWSPuml/Database/DynamoDBTable.puml

actor User as user
IoTAlexaSkill(onecall, OneCall Timer, "ex) Amazon Echo")
Lambda(timer, Timer Lambda, Lambda)
LambdaLambdaFunction(receiver, Timer Receiver, receive)
LambdaLambdaFunction(attacker, Timer Attacker, attack)
DynamoDB(user_db, User DB, DB)
DynamoDBTable(user_table, user-table, record timer)

user - onecall
onecall - timer
timer - user_db

timer +-- receiver
timer +-- attacker

user_db +-- user_table

@enduml
```
