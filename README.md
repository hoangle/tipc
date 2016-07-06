# tipc util commands (former tipc-config)

cat safplus/etc/asp.conf | grep "TIPC_NETID\|LINK_NAME\|DEFAULT_NODEADDR"
# DEFAULT_NODEADDR - This is the slot number that will be used for this node.
export DEFAULT_NODEADDR=1
# based, the node address will fall back to the definition in DEFAULT_NODEADDR.
# LINK_NAME - This is the name of network device to be used by the cluster.
export LINK_NAME=eth1
# TIPC_NETID - The netid is used by tipc to keep different clusters separate.
# each have a unique TIPC_NETID number.  This value is originally set based 
export TIPC_NETID=5460

=> tipc-config is deprecated since linux kernel 4.0.0, using tipc instead

> modprobe tipc      => load tipc module
> modprobe -r tipc   => unload tipc module

1. tipc-config -netid=$TIPC_NETID -addr=1.1.$DEFAULT_NODEADDR -be=eth:$LINK_NAME
> tipc node set netid $TIPC_NETID
> tipc node set address 1.1.$DEFAULT_NODEADDR
> tipc bearer enable media eth device $LINK_NAME

2. tipc-config -ls
> tipc link tipc statistics show

3. tipc-config -nt
> tipc nametable show

4. tipc -bd=eth:$LINK_NAME
> tipc bearer disable media eth device $LINK_NAME

5. tipc-config -lw=eth:$LINK_NAME/500 -lt=eth:$LINK_NAME/5000
> tipc bearer set tolerance 5000 media eth device $LINK_NAME

> tipc bearer set window 500 media eth device $LINK_NAME

> tipc bearer set priority 1 media eth device $LINK_NAME

6. Example:
> modprobe tipc
> tipc node set netid 5460
> tipc node set address 1.1.1
> tipc bearer enable media eth device eth1
