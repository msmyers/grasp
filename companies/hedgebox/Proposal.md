# Hedgebox

A turn-key toolkit for your personal Hedgefund in a Box.

### How to install
```
yarn global add @hedgebox/kit

hbox get-started
    > Fetching identity from github ... Welcome @msmyers! [ github.com
    > Creating hbox.com/@msmyers    ... done!           [ hbox.com/@msmyers         ]
    > Fetching manifests            ... done!           [ hbox.com/inspect/6BA0BAEE ]
    > Checking docker               ... done!           [ pid: 345                  ]
    > Generate Hedgekit             ... @hbox/kit:kits  [ hbox.com/inspect/A06BA0BC ]
        - hbox/keys                 ... @hbox/kit:keys  [ hbox.com/inspect/C06BA0BA ]
        - hbox/conn                 ... @hbox/kit:conn  [ hbox.com/inspect/AE30AE30 ]
        - hbox/exec                 ... @hbox/kit:exec  [ hbox.com/inspect/A06BA0BC ]
        - hbox/algo                 ... downloading...  [ @hbox/kit:algo#EBC0BC03 ]  
        - hbox/indy                 ... downloading...  [ @hbox/kit:indy#0BC0BC03 ]  
        - hbox/dash                 ... waiting
        - hbox/repo                 ... waiting
        - hbox/sell                 ... waiting
```

### How to see what's up

```bash
# list one algo
docker images -f reference=@hbox/algo#rev34
# list all algo
docker images -f reference=@hbox/algo
# list all things
docker images -f reference=@hbox
```

### How to create a new indicator
```bash
hbox create indicator mything

#    > Fetching template "default"   ... done!
#    > Unboxing                      ... done! [ hbox.com/inspect/3474744 ]
#    > Building                      ... done! [ docker images -f reference=@msmyers/indy:mything ]
#
#      Ready!
# 
#      Learn more at hbox.com/learn/indicator
#  
#      Get started with "vim mything/indicator.kt"
```

### How to setup keys

```bash
hbox exchanges

#   What exchange would you like? _  
#      (help: hbox.com/exchanges)
#
#   What is your access key? _
#      (help: hbox.com/keys)
#
#   Verifying...         [ done! ]
#
#   Your keys have been saved within @hbox/kit:keys
#    
#   1. To clear keys, use `hbox keys clear`
#   2. To admin keys, use `hbox keys rules`
#   3. To stall keys, use `hbox keys stall`
#   4. To check keys, use `hbox keys check`
#   5. To audit keys, use `hbox keys audit`
#   6. To share keys, use `hbox keys share`
```

### How to run your shit

```bash
# run with settings file
HBOX_PLAN=./mything/myplan.yml hbox ...

# test anything, with defaults
> hbox test             # run it general

# test anything, with duration
> hbox test back=30d    # run backtested

# test buy algo (all params optional)
> hbox test want=BTC have=$30k on=bittrex back=50d every=1m 

# run your shit local
> hbox run local on=bittrex want=BTC have=USD every=1m until="15%|$40k|-10%|3hours" while="sentiment > 10%" \ 
                 mfa=3345

# run remote
> hbox run cloud on=bittrex ...same...

# run remote costs money, so setup a fee budget
> hbox run cloud on=... budget=$30
    #        this box running: hbox.com/@msmyers/myproject/status?revision=3478463
    #      everything running: hbox.com/@msmyers/status
    #       (status pages are only visible to you)
```

### How to publish your shit

```bash
# required: person/name
# optional: person/name:revision#signature
# possible: github styles: 
hbox clone @msmyers/MACD:45453#3464383;

# go with git-centric/familiar (hbox should be wrapper around git)
$ hbox clone https://github.com/libgit2/libgit2
$ hbox clone git://github.com/libgit2/libgit2
$ hbox clone git@github.com:msmyers/hbox-MACD.git
$ hbox clone msmyers@hbox.com:hbox-MACD.git
$ hbox clone msmyers@hbox.com:hbox-MACD
$ hbox clone @msmyers/hbox-MACD

$ hbox pull
$ hbox commit 
$ hbox push
```

### How to make money
```bash

# how to make money by selling
> hbox offerings enable 
    # Success! Marked as offered  : hbox.com/@msmyers/myproject
    #          See who's tried it : hbox.com/@msmyers/myproject/tried?within=30d
    #          See who's using it : hbox.com/@msmyers/myproject/using
    #          How you're paid    : hbox.com/@msmyers/myproject/running   
 
# how to see how your offerings are going
> hbox offerings

```

### Discussion

```
 * Things we need to get right:
    - turn-key/enjoyable process, from install to first-indicator
    - beautiful charts/ui within Dashboard
    - Must "pair words to "action" (beautiful match of "form/function")
    - Must "feel good" to "get started"
    - Must "feel safe" to "try someone"
    - Must "look good" to "get friends"

    - We need to have the BEST backtesting data

    - We need to have online profiles for Algo, Person, and Session
        * search: hbox.com/algos
        * filter: hbox.com/algos/MACD           (list all in that category
        * choose: hbox.com/algos/MACD/best      
        * choose: hbox.com/algos/MACD/latest      

    - We need to be as clean/minimal as github
    - We need to allow for easy sharing snippets

 * We neeed to have 3 examples of every "category" of thing (Indicator, Algo, Alert, etc)

 * Languages
    - Ideal : Python, Kotlin, ES6
    - Desire: Kotlin (with easy bridge into Python/ES6 libraries)
    - Likely: Python, off-the-shelf
       (NOTE: kotlin can be signed/secured. Python/ES6 are editable after deploy)

 * Docker
    - the containers will cross-talk, thru docker-compose network rules
    - the containers will self-destruct if someone docker-exec's in
    - the containers will be signed

 * repos        
    - we'll be a git-compatible host
    - we'll be a docker-hub host
```

### Research

 * engines:
   - https://burnermachine.com/#/
   
 * algo:predict:
   - https://towardsdatascience.com/cryptocurrency-price-prediction-using-deep-learning-70cfca50dd3a
   
 * competitor(ish): 
   - https://github.com/quantopian/zipline
   - https://enigma.co/catalyst/
   - https://enigma.co/catalyst/example-algos.html#buy-btc-simple-algorithm
   
 
 * storefront: 
   - https://frappe.io/marketplace
   - https://github.com/0xProject/0x-launch-kit
 
 * storage:time-series: 
   - https://medium.com/kudos-engineering/choosing-the-elastic-stack-as-a-time-series-database-9fac202c53ba
   - https://dzone.com/articles/influxdb-vs-elasticsearch-for-time-series-analysis
   - https://www.elastic.co/blog/elasticsearch-as-a-time-series-data-store

 * data:
   - gather: act on: https://www.influxdata.com/
   
 * vault:
   - https://github.com/hashicorp/docker-vault
   - https://blog.ruanbekker.com/blog/2019/05/06/setup-hashicorp-vault-server-on-docker-and-cli-guide/
   - https://medium.com/@maxy_ermayank/credential-store-using-hashicorp-vault-7d2fdeed08f2
   - https://www.hashicorp.com/resources/securing-container-secrets-vault

 * algo:examples:
   - elasticsearch:moving-avg: 
     * https://www.elastic.co/blog/staying-in-control-with-moving-averages-part-1
     * https://www.elastic.co/blog/staying-in-control-with-moving-averages-part-2
   - elasticsearch:aggregation: 
     * https://www.elastic.co/guide/en/elasticsearch/reference/master/search-aggregations-pipeline-movfn-aggregation.html
     