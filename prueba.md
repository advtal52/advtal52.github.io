@startuml
title PROVISION
actor TECNICO

box CRM
participant OMS
end box

box "SERVICE ORDER MANAGER"
participant ESB
participant SOM
end box

box "PREFA"
participant IRED
participant SINPLEX
end box

box "PROVISION / PLATAFORMAS"
participant INVENTARIO_RR
participant ACTIVADOR
participant NM
participant OLT
participant PSA
participant IMS
participant ALVCC
participant ACS
participant SERVER_TPTP
participant TV
end box

box "INSTALACION"
participant TOA
participant INSTALACIONES
end box


TECNICO->OMS:carga
activate OMS
OMS->ESB:
deactivate OMS
activate ESB
ESB->IRED:
deactivate ESB
activate IRED
note right of IRED:prefa:\n(el pelo tien que estar\n marcado como disponible\npara velocidades\nhasta 2500 mb/s)
IRED->SINPLEX: Prefa
deactivate IRED
activate SINPLEX
SINPLEX-->IRED:arma oferta
deactivate SINPLEX
activate IRED
IRED-->ESB:
deactivate IRED
activate ESB
ESB-->OMS:
deactivate ESB
activate OMS
OMS->TOA:agenda cita
deactivate OMS
activate TOA
TOA-->OMS:
deactivate TOA
activate OMS
OMS->SOM:
deactivate OMS
activate SOM
SOM->IRED:diseño
deactivate SOM
activate IRED
IRED->INVENTARIO_RR:pelo FO, plan
deactivate IRED
activate INVENTARIO_RR
note right of INVENTARIO_RR :reseva el recurso
INVENTARIO_RR-->IRED: OLT, VLAN, PSA..
deactivate INVENTARIO_RR
activate IRED
IRED-->SOM:
deactivate IRED
activate SOM
note left of SOM :Orden para creacion de BA
SOM->ACTIVADOR:rden creacion de BA (OLT, user, VLAN, PSA, plan...)
deactivate SOM
activate ACTIVADOR
ACTIVADOR->NM:
deactivate ACTIVADOR
activate NM
NM->OLT:configurar servicios
deactivate NM
activate OLT
OLT-->NM:
deactivate OLT
activate NM
NM-->ACTIVADOR:
deactivate NM
activate ACTIVADOR
ACTIVADOR->PSA:cargar cuenta
deactivate ACTIVADOR
activate PSA
PSA-->ACTIVADOR:
deactivate PSA
activate ACTIVADOR
ACTIVADOR-->SOM:
deactivate ACTIVADOR
activate SOM
SOM->ACTIVADOR: Orden de creacion de VoIP
deactivate SOM
activate ACTIVADOR
ACTIVADOR->ALVCC:
deactivate ACTIVADOR
activate ALVCC
alt si
deactivate ALVCC
activate SERVER_TPTP
ALVCC-->SERVER_TPTP:
deactivate SERVER_TPTP
activate ACS
else si no
ACS-->ALVCC:
deactivate ACS
end
activate ALVCC
ALVCC-->ACS:
ALVCC-->IMS:
deactivate ALVCC
activate IMS
IMS-->ALVCC:
deactivate IMS
activate ALVCC
ALVCC-->ACTIVADOR:
deactivate ALVCC
activate ACTIVADOR
ACTIVADOR-->SOM:
deactivate ACTIVADOR
activate SOM
SOM-->ACTIVADOR:
deactivate SOM
activate ACTIVADOR
ACTIVADOR-->TV:
deactivate ACTIVADOR
activate TV
TV-->ACTIVADOR:
deactivate TV
activate ACTIVADOR
ACTIVADOR-->PSA:
deactivate ACTIVADOR
activate PSA
PSA-->ACTIVADOR:
deactivate PSA
activate ACTIVADOR
ACTIVADOR-->SOM:
deactivate ACTIVADOR
activate SOM
SOM-->TOA:
deactivate SOM
activate TOA
TOA-->INSTALACIONES:
deactivate TOA
activate INSTALACIONES
INSTALACIONES-->TOA:
deactivate INSTALACIONES
activate TOA
TOA-->SOM:
deactivate TOA
activate SOM
SOM-->IRED:
deactivate SOM
activate IRED
IRED-->SOM:
deactivate IRED
activate SOM
SOM-->OMS:
deactivate SOM
@enduml
