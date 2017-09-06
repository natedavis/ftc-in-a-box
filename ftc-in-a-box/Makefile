FEATHERCOIN=feathercoind
FEATHERCOINCLI=feathercoin-cli
B1_FLAGS=
B2_FLAGS=
B1=-datadir=1 $(B1_FLAGS)
B2=-datadir=2 $(B2_FLAGS)
BLOCKS=1
ADDRESS=
AMOUNT=
ACCOUNT=

start:
	$(FEATHERCOIN) $(B1) -daemon
	$(FEATHERCOIN) $(B2) -daemon

generate:
	$(FEATHERCOINCLI) $(B1) setgenerate true $(BLOCKS)

getinfo:
	$(FEATHERCOINCLI) $(B1) getinfo
	$(FEATHERCOINCLI) $(B2) getinfo

sendfrom1:
	$(FEATHERCOINCLI) $(B1) sendtoaddress $(ADDRESS) $(AMOUNT)

sendfrom2:
	$(FEATHERCOINCLI) $(B2) sendtoaddress $(ADDRESS) $(AMOUNT)

address1:
	$(FEATHERCOINCLI) $(B1) getnewaddress $(ACCOUNT)

address2:
	$(FEATHERCOINCLI) $(B2) getnewaddress $(ACCOUNT)

stop:
	$(FEATHERCOINCLI) $(B1) stop
	$(FEATHERCOINCLI) $(B2) stop

clean:
	find 1/regtest/* -not -name 'server.*' -delete
	find 2/regtest/* -not -name 'server.*' -delete