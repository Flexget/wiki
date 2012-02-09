= Sleep =

Sleep between feed executions, useful pretty much only when you have multiple feeds accessing same domain and you want to maintain minimum request interval. For within same feed you can use [wiki:Plugins/domain_delay domain_delay].

Configuration:

{{{
sleep: <seconds>
}}}


