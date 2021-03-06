Module gproc
============


<h1>Module gproc</h1>

* [Description](#description)
* [Data Types](#types)
* [Function Index](#index)
* [Function Details](#functions)


Extended process registry.



__Behaviours:__ [`gen_server`](gen_server.md).

__Authors:__ Ulf Wiger ([`ulf.wiger@erlang-consulting.com`](mailto:ulf.wiger@erlang-consulting.com)).

<h2><a name="description">Description</a></h2>



This module implements an extended process registry


For a detailed description, see
[erlang07-wiger.pdf](erlang07-wiger.pdf).

Type and scope for registration and lookup:



<h2><a name="types">Data Types</a></h2>





<h3 class="typedecl"><a name="type-context">context()</a></h3>




<pre>context() = {<a href="#type-scope">scope()</a>, <a href="#type-type">type()</a>} | <a href="#type-type">type()</a></pre>


{'all','all'} is the default



<h3 class="typedecl"><a name="type-headpat">headpat()</a></h3>




<pre>headpat() = {<a href="#type-keypat">keypat()</a>, <a href="#type-pidpat">pidpat()</a>, ValPat}</pre>



<h3 class="typedecl"><a name="type-key">key()</a></h3>




<pre>key() = {<a href="#type-type">type()</a>, <a href="#type-scope">scope()</a>, any()}</pre>



<h3 class="typedecl"><a name="type-keypat">keypat()</a></h3>




<pre>keypat() = {<a href="#type-sel_type">sel_type()</a> | <a href="#type-sel_var">sel_var()</a>, l | g | <a href="#type-sel_var">sel_var()</a>, any()}</pre>



<h3 class="typedecl"><a name="type-pidpat">pidpat()</a></h3>




<pre>pidpat() = pid() | <a href="#type-sel_var">sel_var()</a></pre>


sel_var() = DollarVar | '_'.


<h3 class="typedecl"><a name="type-scope">scope()</a></h3>




<pre>scope() = l | g</pre>




l = local registration; g = global registration

Type and scope for select(), qlc() and stepping:



<h3 class="typedecl"><a name="type-sel_pattern">sel_pattern()</a></h3>




<pre>sel_pattern() = [{<a href="#type-headpat">headpat()</a>, Guards, Prod}]</pre>



<h3 class="typedecl"><a name="type-sel_scope">sel_scope()</a></h3>




<pre>sel_scope() = scope | all | global | local</pre>



<h3 class="typedecl"><a name="type-sel_type">sel_type()</a></h3>




<pre>sel_type() = <a href="#type-type">type()</a> | names | props | counters | aggr_counters</pre>



<h3 class="typedecl"><a name="type-type">type()</a></h3>




<pre>type() = n | p | c | a</pre>


n = name; p = property; c = counter;
a = aggregate_counter

<h2><a name="index">Function Index</a></h2>



<table width="100%" border="1" cellspacing="0" cellpadding="2" summary="function index"><tr><td valign="top"><a href="#add_global_aggr_counter-1">add_global_aggr_counter/1</a></td><td>Registers a global (unique) aggregated counter.</td></tr><tr><td valign="top"><a href="#add_global_counter-2">add_global_counter/2</a></td><td>Registers a global (non-unique) counter.</td></tr><tr><td valign="top"><a href="#add_global_name-1">add_global_name/1</a></td><td>Registers a global (unique) name.</td></tr><tr><td valign="top"><a href="#add_global_property-2">add_global_property/2</a></td><td>Registers a global (non-unique) property.</td></tr><tr><td valign="top"><a href="#add_local_aggr_counter-1">add_local_aggr_counter/1</a></td><td>Registers a local (unique) aggregated counter.</td></tr><tr><td valign="top"><a href="#add_local_counter-2">add_local_counter/2</a></td><td>Registers a local (non-unique) counter.</td></tr><tr><td valign="top"><a href="#add_local_name-1">add_local_name/1</a></td><td>Registers a local (unique) name.</td></tr><tr><td valign="top"><a href="#add_local_property-2">add_local_property/2</a></td><td>Registers a local (non-unique) property.</td></tr><tr><td valign="top"><a href="#audit_process-1">audit_process/1</a></td><td></td></tr><tr><td valign="top"><a href="#await-1">await/1</a></td><td>Equivalent to <a href="#await-2"><tt>await(Key, infinity)</tt></a>.</td></tr><tr><td valign="top"><a href="#await-2">await/2</a></td><td>Wait for a local name to be registered.</td></tr><tr><td valign="top"><a href="#cancel_wait-2">cancel_wait/2</a></td><td></td></tr><tr><td valign="top"><a href="#default-1">default/1</a></td><td></td></tr><tr><td valign="top"><a href="#first-1">first/1</a></td><td>Behaves as ets:first(Tab) for a given type of registration object.</td></tr><tr><td valign="top"><a href="#get_value-1">get_value/1</a></td><td>Read the value stored with a key registered to the current process.</td></tr><tr><td valign="top"><a href="#give_away-2">give_away/2</a></td><td>Atomically transfers the key <code>From</code> to the process identified by <code>To</code>.</td></tr><tr><td valign="top"><a href="#info-1">info/1</a></td><td>Similar to <code>process_info(Pid)</code> but with additional gproc info.</td></tr><tr><td valign="top"><a href="#info-2">info/2</a></td><td>Similar to process_info(Pid, Item), but with additional gproc info.</td></tr><tr><td valign="top"><a href="#last-1">last/1</a></td><td>Behaves as ets:last(Tab) for a given type of registration object.</td></tr><tr><td valign="top"><a href="#lookup_global_aggr_counter-1">lookup_global_aggr_counter/1</a></td><td>Lookup a global (unique) aggregated counter and returns its value.</td></tr><tr><td valign="top"><a href="#lookup_global_counters-1">lookup_global_counters/1</a></td><td>Look up all global (non-unique) instances of a given Counter.</td></tr><tr><td valign="top"><a href="#lookup_global_name-1">lookup_global_name/1</a></td><td>Lookup a global unique name.</td></tr><tr><td valign="top"><a href="#lookup_global_properties-1">lookup_global_properties/1</a></td><td>Look up all global (non-unique) instances of a given Property.</td></tr><tr><td valign="top"><a href="#lookup_local_aggr_counter-1">lookup_local_aggr_counter/1</a></td><td>Lookup a local (unique) aggregated counter and returns its value.</td></tr><tr><td valign="top"><a href="#lookup_local_counters-1">lookup_local_counters/1</a></td><td>Look up all local (non-unique) instances of a given Counter.</td></tr><tr><td valign="top"><a href="#lookup_local_name-1">lookup_local_name/1</a></td><td>Lookup a local unique name.</td></tr><tr><td valign="top"><a href="#lookup_local_properties-1">lookup_local_properties/1</a></td><td>Look up all local (non-unique) instances of a given Property.</td></tr><tr><td valign="top"><a href="#lookup_pid-1">lookup_pid/1</a></td><td>Lookup the Pid stored with a key.</td></tr><tr><td valign="top"><a href="#lookup_pids-1">lookup_pids/1</a></td><td>Returns a list of pids with the published key Key.</td></tr><tr><td valign="top"><a href="#lookup_value-1">lookup_value/1</a></td><td>Lookup the value stored with a key.</td></tr><tr><td valign="top"><a href="#lookup_values-1">lookup_values/1</a></td><td>Retrieve the <code>{Pid,Value}</code> pairs corresponding to Key.</td></tr><tr><td valign="top"><a href="#mreg-3">mreg/3</a></td><td>Register multiple {Key,Value} pairs of a given type and scope.</td></tr><tr><td valign="top"><a href="#nb_wait-1">nb_wait/1</a></td><td>Wait for a local name to be registered.</td></tr><tr><td valign="top"><a href="#next-2">next/2</a></td><td>Behaves as ets:next(Tab,Key) for a given type of registration object.</td></tr><tr><td valign="top"><a href="#prev-2">prev/2</a></td><td>Behaves as ets:prev(Tab,Key) for a given type of registration object.</td></tr><tr><td valign="top"><a href="#reg-1">reg/1</a></td><td>Equivalent to <a href="#reg-2"><tt>reg(Key, default(Key))</tt></a>.</td></tr><tr><td valign="top"><a href="#reg-2">reg/2</a></td><td>Register a name or property for the current process.</td></tr><tr><td valign="top"><a href="#select-1">select/1</a></td><td>Equivalent to <a href="#select-2"><tt>select(all, Pat)</tt></a>.</td></tr><tr><td valign="top"><a href="#select-2">select/2</a></td><td>Perform a select operation on the process registry.</td></tr><tr><td valign="top"><a href="#select-3">select/3</a></td><td>Like <a href="#select-2"><code>select/2</code></a> but returns Limit objects at a time.</td></tr><tr><td valign="top"><a href="#send-2">send/2</a></td><td>Sends a message to the process, or processes, corresponding to Key.</td></tr><tr><td valign="top"><a href="#set_value-2">set_value/2</a></td><td>Sets the value of the registeration entry given by Key.</td></tr><tr><td valign="top"><a href="#start_link-0">start_link/0</a></td><td>Starts the gproc server.</td></tr><tr><td valign="top"><a href="#table-1">table/1</a></td><td>Equivalent to <a href="#table-2"><tt>table(Context, [])</tt></a>.</td></tr><tr><td valign="top"><a href="#table-2">table/2</a></td><td>QLC table generator for the gproc registry.</td></tr><tr><td valign="top"><a href="#unreg-1">unreg/1</a></td><td>Unregister a name or property.</td></tr><tr><td valign="top"><a href="#unregister_name-1">unregister_name/1</a></td><td>Equivalent to <tt>unreg / 1</tt>.</td></tr><tr><td valign="top"><a href="#update_counter-2">update_counter/2</a></td><td>Updates the counter registered as Key for the current process.</td></tr><tr><td valign="top"><a href="#where-1">where/1</a></td><td>Returns the pid registered as Key.</td></tr><tr><td valign="top"><a href="#whereis_name-1">whereis_name/1</a></td><td>Equivalent to <tt>where / 1</tt>.</td></tr></table>




<h2><a name="functions">Function Details</a></h2>


<a name="add_global_aggr_counter-1"></a>

<h3>add_global_aggr_counter/1</h3>





`add_global_aggr_counter(Name) -> any()`



Equivalent to [`reg({a, g, Name})`](#reg-1).

Registers a global (unique) aggregated counter.<a name="add_global_counter-2"></a>

<h3>add_global_counter/2</h3>





`add_global_counter(Name, Initial) -> any()`



Registers a global (non-unique) counter. @equiv reg({c,g,Name},Value)<a name="add_global_name-1"></a>

<h3>add_global_name/1</h3>





`add_global_name(Name) -> any()`



Registers a global (unique) name. @equiv reg({n,g,Name})<a name="add_global_property-2"></a>

<h3>add_global_property/2</h3>





`add_global_property(Name, Value) -> any()`



Registers a global (non-unique) property. @equiv reg({p,g,Name},Value)<a name="add_local_aggr_counter-1"></a>

<h3>add_local_aggr_counter/1</h3>





`add_local_aggr_counter(Name) -> any()`



Equivalent to [`reg({a, l, Name})`](#reg-1).

Registers a local (unique) aggregated counter.<a name="add_local_counter-2"></a>

<h3>add_local_counter/2</h3>





`add_local_counter(Name, Initial) -> any()`



Registers a local (non-unique) counter. @equiv reg({c,l,Name},Value)<a name="add_local_name-1"></a>

<h3>add_local_name/1</h3>





`add_local_name(Name) -> any()`



Registers a local (unique) name. @equiv reg({n,l,Name})<a name="add_local_property-2"></a>

<h3>add_local_property/2</h3>





`add_local_property(Name, Value) -> any()`



Registers a local (non-unique) property. @equiv reg({p,l,Name},Value)<a name="audit_process-1"></a>

<h3>audit_process/1</h3>





<pre>audit_process(Pid::pid()) -> ok</pre>
<br></br>


<a name="await-1"></a>

<h3>await/1</h3>





<pre>await(Key::<a href="#type-key">key()</a>) -> {pid(), Value}</pre>
<br></br>




Equivalent to [`await(Key, infinity)`](#await-2).<a name="await-2"></a>

<h3>await/2</h3>





<pre>await(Key::<a href="#type-key">key()</a>, Timeout) -> {pid(), Value}</pre>
<ul class="definitions"><li><pre>Timeout = integer() | infinity</pre></li></ul>



Wait for a local name to be registered.
The function raises an exception if the timeout expires. Timeout must be
either an interger > 0 or 'infinity'.
A small optimization: we first perform a lookup, to see if the name
is already registered. This way, the cost of the operation will be
roughly the same as of where/1 in the case where the name is already
registered (the difference: await/2 also returns the value).<a name="cancel_wait-2"></a>

<h3>cancel_wait/2</h3>





`cancel_wait(Key, Ref) -> any()`

<a name="default-1"></a>

<h3>default/1</h3>





`default(X1) -> any()`

<a name="first-1"></a>

<h3>first/1</h3>





<pre>first(Context::<a href="#type-context">context()</a>) -> <a href="#type-key">key()</a> | '$end_of_table'</pre>
<br></br>






Behaves as ets:first(Tab) for a given type of registration object.

See [`http://www.erlang.org/doc/man/ets.html#first-1`](http://www.erlang.org/doc/man/ets.html#first-1).
The registry behaves as an ordered_set table.<a name="get_value-1"></a>

<h3>get_value/1</h3>





<pre>get_value(Key) -> Value</pre>
<br></br>






Read the value stored with a key registered to the current process.

If no such key is registered to the current process, this function exits.<a name="give_away-2"></a>

<h3>give_away/2</h3>





<pre>give_away(From::<a href="#type-key">key()</a>, To::pid() | <a href="#type-key">key()</a>) -> undefined | pid()</pre>
<br></br>






Atomically transfers the key `From` to the process identified by `To`.



This function transfers any gproc key (name, property, counter, aggr. counter)  
from one process to another, and returns the pid of the new owner.



`To` must be either a pid or a unique name (name or aggregated counter), but
does not necessarily have to resolve to an existing process. If there is
no process registered with the `To` key, `give_away/2` returns `undefined`,
and the `From` key is effectively unregistered.



It is allowed to give away a key to oneself, but of course, this operation  
will have no effect.

Fails with `badarg` if the calling process does not have a `From` key
registered.<a name="info-1"></a>

<h3>info/1</h3>





<pre>info(Pid::pid()) -> ProcessInfo</pre>
<ul class="definitions"><li><pre>ProcessInfo = [{gproc, [{Key, Value}]} | ProcessInfo]</pre></li></ul>





Similar to `process_info(Pid)` but with additional gproc info.

Returns the same information as process_info(Pid), but with the
addition of a `gproc` information item, containing the `{Key,Value}`
pairs registered to the process.<a name="info-2"></a>

<h3>info/2</h3>





<pre>info(Pid::pid(), Item::atom()) -> {Item, Info}</pre>
<br></br>






Similar to process_info(Pid, Item), but with additional gproc info.

For `Item = gproc`, this function returns a list of `{Key, Value}` pairs
registered to the process Pid. For other values of Item, it returns the
same as [`http://www.erlang.org/doc/man/erlang.html#process_info-2`](http://www.erlang.org/doc/man/erlang.html#process_info-2).<a name="last-1"></a>

<h3>last/1</h3>





<pre>last(Context::<a href="#type-context">context()</a>) -> <a href="#type-key">key()</a> | '$end_of_table'</pre>
<br></br>






Behaves as ets:last(Tab) for a given type of registration object.

See [`http://www.erlang.org/doc/man/ets.html#last-1`](http://www.erlang.org/doc/man/ets.html#last-1).
The registry behaves as an ordered_set table.<a name="lookup_global_aggr_counter-1"></a>

<h3>lookup_global_aggr_counter/1</h3>





<pre>lookup_global_aggr_counter(Name::any()) -> integer()</pre>
<br></br>




Equivalent to [`where({a, g, Name})`](#where-1).

Lookup a global (unique) aggregated counter and returns its value.
Fails if there is no such object.<a name="lookup_global_counters-1"></a>

<h3>lookup_global_counters/1</h3>





<pre>lookup_global_counters(Counter::any()) -> [{pid(), Value::integer()}]</pre>
<br></br>




Equivalent to [`lookup_values({c, g, Counter})`](#lookup_values-1).

Look up all global (non-unique) instances of a given Counter.
Returns a list of {Pid, Value} tuples for all matching objects.<a name="lookup_global_name-1"></a>

<h3>lookup_global_name/1</h3>





<pre>lookup_global_name(Name::any()) -> pid()</pre>
<br></br>




Equivalent to [`where({n, g, Name})`](#where-1).

Lookup a global unique name. Fails if there is no such name.<a name="lookup_global_properties-1"></a>

<h3>lookup_global_properties/1</h3>





<pre>lookup_global_properties(Property::any()) -> [{pid(), Value}]</pre>
<br></br>




Equivalent to [`lookup_values({p, g, Property})`](#lookup_values-1).

Look up all global (non-unique) instances of a given Property.
Returns a list of {Pid, Value} tuples for all matching objects.<a name="lookup_local_aggr_counter-1"></a>

<h3>lookup_local_aggr_counter/1</h3>





<pre>lookup_local_aggr_counter(Name::any()) -> integer()</pre>
<br></br>




Equivalent to [`where({a, l, Name})`](#where-1).

Lookup a local (unique) aggregated counter and returns its value.
Fails if there is no such object.<a name="lookup_local_counters-1"></a>

<h3>lookup_local_counters/1</h3>





<pre>lookup_local_counters(Counter::any()) -> [{pid(), Value::integer()}]</pre>
<br></br>




Equivalent to [`lookup_values({c, l, Counter})`](#lookup_values-1).

Look up all local (non-unique) instances of a given Counter.
Returns a list of {Pid, Value} tuples for all matching objects.<a name="lookup_local_name-1"></a>

<h3>lookup_local_name/1</h3>





<pre>lookup_local_name(Name::any()) -> pid()</pre>
<br></br>




Equivalent to [`where({n, l, Name})`](#where-1).

Lookup a local unique name. Fails if there is no such name.<a name="lookup_local_properties-1"></a>

<h3>lookup_local_properties/1</h3>





<pre>lookup_local_properties(Property::any()) -> [{pid(), Value}]</pre>
<br></br>




Equivalent to [`lookup_values({p, l, Property})`](#lookup_values-1).

Look up all local (non-unique) instances of a given Property.
Returns a list of {Pid, Value} tuples for all matching objects.<a name="lookup_pid-1"></a>

<h3>lookup_pid/1</h3>





<pre>lookup_pid(Key) -> Pid</pre>
<br></br>




Lookup the Pid stored with a key.
<a name="lookup_pids-1"></a>

<h3>lookup_pids/1</h3>





<pre>lookup_pids(Key::<a href="#type-key">key()</a>) -> [pid()]</pre>
<br></br>






Returns a list of pids with the published key Key

If the type of registration entry is either name or aggregated counter,
this function will return either an empty list, or a list of one pid.
For non-unique types, the return value can be a list of any length.<a name="lookup_value-1"></a>

<h3>lookup_value/1</h3>





<pre>lookup_value(Key) -> Value</pre>
<br></br>




Lookup the value stored with a key.
<a name="lookup_values-1"></a>

<h3>lookup_values/1</h3>





<pre>lookup_values(Key::<a href="#type-key">key()</a>) -> [{pid(), Value}]</pre>
<br></br>






Retrieve the `{Pid,Value}` pairs corresponding to Key.

Key refer to any type of registry object. If it refers to a unique
object, the list will be of length 0 or 1. If it refers to a non-unique
object, the return value can be a list of any length.<a name="mreg-3"></a>

<h3>mreg/3</h3>





<pre>mreg(T::<a href="#type-type">type()</a>, X2::<a href="#type-scope">scope()</a>, KVL::[{Key::any(), Value::any()}]) -> true</pre>
<br></br>






Register multiple {Key,Value} pairs of a given type and scope.

This function is more efficient than calling [`reg/2`](#reg-2) repeatedly.<a name="nb_wait-1"></a>

<h3>nb_wait/1</h3>





<pre>nb_wait(Key::<a href="#type-key">key()</a>) -> Ref</pre>
<br></br>




Wait for a local name to be registered.
The caller can expect to receive a message,
{gproc, Ref, registered, {Key, Pid, Value}}, once the name is registered.<a name="next-2"></a>

<h3>next/2</h3>





<pre>next(Context::<a href="#type-context">context()</a>, Key::<a href="#type-key">key()</a>) -> <a href="#type-key">key()</a> | '$end_of_table'</pre>
<br></br>






Behaves as ets:next(Tab,Key) for a given type of registration object.

See [`http://www.erlang.org/doc/man/ets.html#next-2`](http://www.erlang.org/doc/man/ets.html#next-2).
The registry behaves as an ordered_set table.<a name="prev-2"></a>

<h3>prev/2</h3>





<pre>prev(Context::<a href="#type-context">context()</a>, Key::<a href="#type-key">key()</a>) -> <a href="#type-key">key()</a> | '$end_of_table'</pre>
<br></br>






Behaves as ets:prev(Tab,Key) for a given type of registration object.

See [`http://www.erlang.org/doc/man/ets.html#prev-2`](http://www.erlang.org/doc/man/ets.html#prev-2).
The registry behaves as an ordered_set table.<a name="reg-1"></a>

<h3>reg/1</h3>





<pre>reg(Key::<a href="#type-key">key()</a>) -> true</pre>
<br></br>




Equivalent to [`reg(Key, default(Key))`](#reg-2).<a name="reg-2"></a>

<h3>reg/2</h3>





<pre>reg(Key::<a href="#type-key">key()</a>, Value) -> true</pre>
<br></br>






Register a name or property for the current process

<a name="select-1"></a>

<h3>select/1</h3>





<pre>select(Pat::<a href="#type-select_pattern">select_pattern()</a>) -> [<a href="#type-sel_object">sel_object()</a>]</pre>
<br></br>




Equivalent to [`select(all, Pat)`](#select-2).<a name="select-2"></a>

<h3>select/2</h3>





<pre>select(Context::<a href="#type-context">context()</a>, Pat::<a href="#type-sel_pattern">sel_pattern()</a>) -> [{Key, Pid, Value}]</pre>
<br></br>






Perform a select operation on the process registry.

The physical representation in the registry may differ from the above,
but the select patterns are transformed appropriately.<a name="select-3"></a>

<h3>select/3</h3>





<pre>select(Context::<a href="#type-context">context()</a>, Pat::<a href="#type-sel_patten">sel_patten()</a>, Limit::integer()) -> [{Key, Pid, Value}]</pre>
<br></br>






Like [`select/2`](#select-2) but returns Limit objects at a time.

See [`http://www.erlang.org/doc/man/ets.html#select-3`](http://www.erlang.org/doc/man/ets.html#select-3).<a name="send-2"></a>

<h3>send/2</h3>





<pre>send(Key::<a href="#type-key">key()</a>, Msg::any()) -> Msg</pre>
<br></br>






Sends a message to the process, or processes, corresponding to Key.

If Key belongs to a unique object (name or aggregated counter), this
function will send a message to the corresponding process, or fail if there
is no such process. If Key is for a non-unique object type (counter or
property), Msg will be send to all processes that have such an object.<a name="set_value-2"></a>

<h3>set_value/2</h3>





<pre>set_value(Key::<a href="#type-key">key()</a>, Value) -> true</pre>
<br></br>






Sets the value of the registeration entry given by Key



Key is assumed to exist and belong to the calling process.  
If it doesn't, this function will exit.

Value can be any term, unless the object is a counter, in which case
it must be an integer.<a name="start_link-0"></a>

<h3>start_link/0</h3>





<pre>start_link() -> {ok, pid()}</pre>
<br></br>






Starts the gproc server.

This function is intended to be called from gproc_sup, as part of
starting the gproc application.<a name="table-1"></a>

<h3>table/1</h3>





<pre>table(Context::<a href="#type-context">context()</a>) -> any()</pre>
<br></br>




Equivalent to [`table(Context, [])`](#table-2).<a name="table-2"></a>

<h3>table/2</h3>





<pre>table(Context::<a href="#type-context">context()</a>, Opts) -> any()</pre>
<br></br>




QLC table generator for the gproc registry.
Context specifies which subset of the registry should be queried.
See [`http://www.erlang.org/doc/man/qlc.html`](http://www.erlang.org/doc/man/qlc.html).<a name="unreg-1"></a>

<h3>unreg/1</h3>





<pre>unreg(Key::<a href="#type-key">key()</a>) -> true</pre>
<br></br>




Unregister a name or property.<a name="unregister_name-1"></a>

<h3>unregister_name/1</h3>





`unregister_name(Key) -> any()`



Equivalent to `unreg / 1`.<a name="update_counter-2"></a>

<h3>update_counter/2</h3>





<pre>update_counter(Key::<a href="#type-key">key()</a>, Incr::integer()) -> integer()</pre>
<br></br>






Updates the counter registered as Key for the current process.

This function works like ets:update_counter/3
(see [`http://www.erlang.org/doc/man/ets.html#update_counter-3`](http://www.erlang.org/doc/man/ets.html#update_counter-3)), but
will fail if the type of object referred to by Key is not a counter.<a name="where-1"></a>

<h3>where/1</h3>





<pre>where(Key::<a href="#type-key">key()</a>) -> pid()</pre>
<br></br>






Returns the pid registered as Key

The type of registration entry must be either name or aggregated counter.
Otherwise this function will exit. Use [`lookup_pids/1`](#lookup_pids-1) in these
cases.<a name="whereis_name-1"></a>

<h3>whereis_name/1</h3>





`whereis_name(Key) -> any()`



Equivalent to `where / 1`.