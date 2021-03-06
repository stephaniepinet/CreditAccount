=== en_US ===


#Credit account

This module is a base for creating module like sponsorship or assets management.

##Installation

```
$ cd local/modules
$ git clone https://github.com/thelia-modules/CreditAccount
```

If you want to download the zip from github, rename the unzip folder as ```CreditAccount```, github suffix the zip and the folder with the current branch name.

After that, you just have to activate the module in your back-office.

## How to use it

In your back-office, on each customer edition page you can add a new credit account.

##Integration

2 loops are available with this module. One for the credit account history and the other one for the current credit account.

A route exists allowing customer to consume his credit account. You just have to call the ```/creditAccount/use``` and the controller will find the credit account for
the current customer and put it in the discount amount.

example in order-invoice.html file, put this block after the postage block :

```
{loop type="credit_account" name="credit_account" customer={customer attr="id"}}
<tr>
    <th class="shipping"><a href="{url path="/creditAccount/use"}">{intl l="Use your credit account"}</a></th>
    <td class="shipping">
        <div class="shipping-price">
            <span class="price">{$CREDIT_AMOUNT} {currency attr="symbol"}</span>
        </div>
    </td>
</tr>
{/loop}
```

##Loops

### Credit account history loop

List the credit account history for a specified credit account

**input argument**

* credit_account : credit account id, it's a mandatory parameter

**output arguments**

* $CREDIT_AMOUNT
* $CREATE_DATE
* $UPDATE_DATE

**example**

```
{loop type="credit_account" name="credit_account_list" customer="{$customer_id}"}
<div class="col-md-12">
    <div class="table-responsive">
        <table class="table table-striped table-left-aligned">
            <thead>
            <tr>
                <th>{intl d="creditaccount.ai" l="amount"}</th>
                <th>{intl d="creditaccount.ai" l="Date & Hour"}</th>
            </tr>
            </thead>
            <tbody>
                {loop type="credit_account_history" name="credit_account_history" credit_account="{$ID}"}
                    <tr>
                        <td>{$CREDIT_AMOUNT}&nbsp;€</td>
                        <td>{format_date date=$CREATE_DATE}</td>
                    </tr>
                {/loop}
            </tbody>

        </table>
    </div>
</div>
{/loop}
```

### Credit account loop

retrieve the current credit account for a specified customer

**input argument**

* customer : customer id, it's a mandatory parameter

**output arguments**

* $ID : credit account id
* $CREDIT_AMOUNT
* $CREATE_DATE
* $UPDATE_DATE

**example**

```
{loop type="credit_account" name="credit_account" customer={customer attr="id"}}
<tr>
    <th class="shipping"><a href="{url path="/creditAccount/use"}">{intl d="creditaccount" l="Use your credit account"}</a></th>
    <td class="shipping">
        <div class="shipping-price">
            <span class="price">{$CREDIT_AMOUNT} {currency attr="symbol"}</span>
        </div>
    </td>
</tr>
{/loop}
```

## Listeners

This module is a base for creating module like sponsorship or assets management. So some listeners are preconfigured for using it in other modules.

### creditAccount.addAccount

This listener is used for adding an amount to a customer's credit account. You have to dispatch a ```CreditAccount\Event\CreditAccountEvent``` class

**Example**

```
//retrieve the dispatcher for using it after. I put it in $dispatcher

// retrieve a customer. For the example I retrieve a random customer, obviously not do that in your application
$customer = \Thelia\Model\CustomerQuery::create()->findOne();

//the amount I want to add to the current customer's credit account
$amount = 10;

// Create the event to dispatch
$event = new \CreditAccount\Event\CreditAccountEvent($customer, $amount)

//dispatch the event
$dispatcher->dispatch(\CreditAccount\CreditAccount::CREDIT_ACCOUNT_ADD_AMOUNT, $event);

```


=== fr_FR ===

#Crédit client

Ce module permet d'ajouter un crédit à chacun de vos clients. 
Il est aussi nécessaire pour des modules du type Fidélisation ou Gestion des avoirs.

##Installation

```
$ cd local/modules
$ git clone https://github.com/thelia-modules/CreditAccount
```

Si vous téléchargez le zip depuis Github, renommer le dossier en ```CreditAccount```. En effet, Github ajoute au répertoire un suffixe avec le nom de la branche. 

Ensuite vous n'avez plus qu'à activer le module dans votre back-office. 


## Utilisation

Dans votre back-office, vous pouvez ajouter pour chaque client un crédit fidélité.
Pour cela, rendez-vous sur la page d'édition du compte client. 


##Intégration

2 boucles sont disponibles pour ce module. 
Une pour l'histoire du crédit client. 
L'autre pour le crédit client courant. 

Pour permettre au client d'utiliser son crédit, une route existe. Il vous suffit d'appeler ```/creditAccount/use```. Le contrôleur trouvera lui-même le crédit du client en question, et l'ajoutera dans le montant de la réduction. 

Par exemple, dans le fichier order-invoice.html, ajoutez le bloc ci-après après le bloc Frais de port:


```
{loop type="credit_account" name="credit_account" customer={customer attr="id"}}
<tr>
    <th class="shipping"><a href="{url path="/creditAccount/use"}">{intl l="Use your credit account"}</a></th>
    <td class="shipping">
        <div class="shipping-price">
            <span class="price">{$CREDIT_AMOUNT} {currency attr="symbol"}</span>
        </div>
    </td>
</tr>
{/loop}
```

##Loops

### Credit account history loop

Liste l'historique des crédits pour un client donné. 

**input argument**

* credit_account : credit account id, paramètre obligatoire

**output arguments**

* $CREDIT_AMOUNT
* $CREATE_DATE
* $UPDATE_DATE

**example**

```
{loop type="credit_account" name="credit_account_list" customer="{$customer_id}"}
<div class="col-md-12">
    <div class="table-responsive">
        <table class="table table-striped table-left-aligned">
            <thead>
            <tr>
                <th>{intl d="creditaccount.ai" l="amount"}</th>
                <th>{intl d="creditaccount.ai" l="Date & Hour"}</th>
            </tr>
            </thead>
            <tbody>
                {loop type="credit_account_history" name="credit_account_history" credit_account="{$ID}"}
                    <tr>
                        <td>{$CREDIT_AMOUNT}&nbsp;€</td>
                        <td>{format_date date=$CREATE_DATE}</td>
                    </tr>
                {/loop}
            </tbody>

        </table>
    </div>
</div>
{/loop}
```

### Credit account loop

Récupère le crédit en cours pour un client donné

**input argument**

* customer : customer id, it's a mandatory parameter

**output arguments**

* $ID : credit account id
* $CREDIT_AMOUNT
* $CREATE_DATE
* $UPDATE_DATE

**example**

```
{loop type="credit_account" name="credit_account" customer={customer attr="id"}}
<tr>
    <th class="shipping"><a href="{url path="/creditAccount/use"}">{intl d="creditaccount" l="Use your credit account"}</a></th>
    <td class="shipping">
        <div class="shipping-price">
            <span class="price">{$CREDIT_AMOUNT} {currency attr="symbol"}</span>
        </div>
    </td>
</tr>
{/loop}
```

## Listeners

Ce module est une base pour créer des modules comme Fidélisation, ou Gestion des avoirs. 
Des "listeners" sont préconfigurés pour être utilisés dans d'autres modules. 


### creditAccount.addAccount

Ce listener est utilisé pour ajouter un montant dans un compte crédit. Vous devez déployer une classe : 
 ```CreditAccount\Event\CreditAccountEvent``` 

**Example**

```
//retrieve the dispatcher for using it after. I put it in $dispatcher

// retrieve a customer. For the example I retrieve a random customer, obviously not do that in your application
$customer = \Thelia\Model\CustomerQuery::create()->findOne();

//the amount I want to add to the current customer's credit account
$amount = 10;

// Create the event to dispatch
$event = new \CreditAccount\Event\CreditAccountEvent($customer, $amount)

//dispatch the event
$dispatcher->dispatch(\CreditAccount\CreditAccount::CREDIT_ACCOUNT_ADD_AMOUNT, $event);

```
