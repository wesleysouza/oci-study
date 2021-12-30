# 4 Identity and Access Management

## IAM Introduction

IAM = Idnetity and Access Management Service
Fine-grained Access Control
AuthN - Who are you?
AuthZ - What permission do you have?

Quem é você? Quais permissões você tem?

Users -> Groups (coleção de usuários do mesmo tipo) -> Service Specific Groups -> Policies (autorizações) -> Compartments -> Resources (dentro dos compartimentos)

Os recursos são objetos da nuvem. 

Each OCI resource is identify with excluvise ID (Unique Oracle-assigned identifier). Oracle Cloud ID (OCID). Example of OCID sintaxe:

```
ocid1.<RESOURCE TYPE>.<REALM>.[REGION][.FUTURE USE].<UNIQUE ID>
```
Realm: set of regions that share entities

Example OCIDs:

-Tenancy:

```
ocid1.tenacy.oc1..aaaaaaaaba3pv6wkcr4jqae5f44n2b2m2yt2j6rx23uzr4h25vqstifsfdsq
```

Block Volume:

```
ocid1.volume.oc1.eu-frankfurt-1.abtheljrwbqhmad266kljreyhbd4p ...
```

## AuthN AuthZ

The IAM entity that is allowed to interact with OCI resources.

Groups are Collection of users with ssame type of access to resources.

### AuthN (IAM authentication)

**"Quem é você?"**

Formas de autenticação:
- API Signing Key
    - Using OCI API + SDK/CLI
    - RSA key pari (PEM)
- Auth Tokens
    - Oracle-generated token strings
    - Authenticate third party APIs

```
begin
    DBMS_CLOUD.create_credential (
        credential_name => 'OBJ_STORE_CRED',
        username => '<userXX>',
        password => '<your Auth Token>'
    );
end;
/
```

### AuthZ (IAM autorização)

Lida com as permissões, quais permissões vc tem?

A autorização é feita por meio de políticas do serviço. Essas políticas são declarações legíveis para humanos que possibilitam definir permissões granulares.

Policies - Human readable statements to define granular permissions

```
Allow group <group_name> to <verb> <resource-type> in tenancy
Allow group <group_name> to <verb> <resource-type> in compartment <compartment_name> [where <conditions>]
```

Policy Attachment - To a compartment or the tenancy

As políticas podem ser atreladas a um compartimento ou a um tenancy. Se estiver atrelada a um compartimento ela será aplicada somente aos recursos so compartimento, se for ao tenacy será aplicada em tudo.

IMPORTANTE: Tudo é negado por padrão, portanto, você não precisa escrever uma instrução para negar algo.

Portanto, você diz que permite _Allow_ <group_name>...

```
Allow group <group_name> to <verb> <resource-type> in tenancy
```

The type of Verbs:
- Manage;
- Use;
- Read;
- Inspect;

| Verb    | Type of access                            | Target User         |
|---------|:------------------------------------------|:--------------------|
| manage  | All permissions for the resource          | Administrators      | 
| use     | read + the actions vary by resource type* | Resources end users |
| read    | inspect + user-specified metadata         | Internal Auditors   |
| inspect | Aability to list resources                | Third-party auditors|

Resources:

| Aggregate resource-type | Individual resource type        |
|-------------------------|:--------------------------------|
| all-resouces            | all                             |
| database-family         | db-systems, db-nodes, databases |
| instance-family         | instances, instance-images, volume-atachments, console-hisoties |
| object-family           | buckets, objects                |
| virtual-network-family  | vcn, subnets, route-tables, security-lists, dhcp-options, and many more resourses |
| volume-family           | volumes, volume-attachments, volume-backups |

### Sumary:

Authenticarion in OCI
- User name / Password
- API Signing Keys
- Authentication tokens

Authorization in OCI
- Policies

## Compartiments

Feature Exclusiva da OCI

Tenancy -> Nome fantasia para a conta

Tenancy/Root Compartment (all resourses).

Você pode criar os seus próprios compartimentos individuais isolando-os dos demais e aplicando diferentes controles de acesso. Esses compartimentos podem conter recursos relacionados. Desse modo, você pode criar um compartimento para recursos de rede, um compartimento para os recursos de armazenamento e etc.

**Best pratice**: Create dedicated compartiments to isolate resources. 

Obs.: Um recurso só pode pertencer a um único compartimento.

Groups + Policies = Acess to Compartments

Razões para usar compartimentos:
- Controlar o acesso e o isolamento;

### Interaction of Resources

Resources can interact with other resources indifferent compartments.

### Movement of Resources

Resources can be moved from one compartment ot another.

Obs.: Compartimentos são contruções globais, como tudo na identidade. Portanto, recursos de várias regiões podem estar no mesmo compartimento.

More for Compartments:
- Six levels of Nesting allowed;
- Set Quotas and Budgets on Compartments


















