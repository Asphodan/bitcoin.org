{% comment %}
This file is licensed under the MIT License (MIT) available on
http://opensource.org/licenses/MIT.
{% endcomment %}
{% assign filename="_includes/ref/bitcoin-core/rpcs/rpcs/lockunspent.md" %}

##### LockUnspent
{% include helpers/subhead-links.md %}

{% assign summary_lockUnspent="temporarily locks or unlocks specified transaction outputs. A locked transaction output will not be chosen by automatic coin selection when spending bitcoins. Locks are stored in memory only, so nodes start with zero locked outputs and the locked output list is always cleared when a node stops or fails." %}

{% autocrossref %}

*Requires wallet support.*

The `lockunspent` RPC {{summary_lockUnspent}}

*Parameter #1---whether to lock or unlock the outputs*

| Name                 | Type            | Presence                    | Description
|----------------------|-----------------|-----------------------------|----------------
| Lock Or Unlock       | bool            | Required<br>(exactly 1)     | Set to `true` to lock the outputs specified in the following parameter.  Set to `false` to unlock the outputs specified.  If this is the only argument specified, all outputs will be unlocked (even if this is set to `false`)
{:.ntpd}

*Parameter #2---the outputs to lock or unlock*

| Name                 | Type            | Presence                    | Description
|----------------------|-----------------|-----------------------------|----------------
| Outputs              | array           | Optional<br>(0 or 1)        | An array of outputs to lock or unlock
| →<br>Output          | object          | Required<br>(1 or more)     | An object describing a particular output
| → →<br>`txid`        | string          | Required<br>(exactly 1)     | The TXID of the transaction containing the output to lock or unlock, encoded as hex in internal byte order
| → →<br>`vout`        | number (int)    | Required<br>(exactly 1)     | The output index number (vout) of the output to lock or unlock.  The first output in a transaction has an index of `0`
{:.ntpd}

*Result---`true` if successful*

| Name                 | Type            | Presence                    | Description
|----------------------|-----------------|-----------------------------|----------------
| `result`             | bool            | Required<br>(exactly 1)     | Set to `true` if the outputs were successfully locked or unlocked
{:.ntpd}

*Example from Bitcoin Core 0.10.0*

Lock two outputs:

{% highlight bash %}
bitcoin-cli -testnet lockunspent true '''
  [
    {
      "txid": "5a7d24cd665108c66b2d56146f244932edae4e2376b561b3d396d5ae017b9589",
      "vout": 0
    },
    {
      "txid": "6c5edd41a33f9839257358ba6ddece67df9db7f09c0db6bbea00d0372e8fe5cd",
      "vout": 0
    }
  ]
'''
{% endhighlight %}

Result:

{% highlight json %}
true
{% endhighlight %}

Unlock one of the above outputs:

{% highlight bash %}
bitcoin-cli -testnet lockunspent false '''
[
  {
    "txid": "5a7d24cd665108c66b2d56146f244932edae4e2376b561b3d396d5ae017b9589",
    "vout": 0
  }
]
'''
{% endhighlight %}

Result:

{% highlight json %}
true
{% endhighlight %}

*See also*

* [ListLockUnspent][rpc listlockunspent]: {{summary_listLockUnspent}}
* [ListUnspent][rpc listunspent]: {{summary_listUnspent}}

{% endautocrossref %}
