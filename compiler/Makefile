
include ../Makefile.conf

all: $(COMPILER)

OBJS=util.cmx dgraph.cmx \
     javascript.cmx js_output.cmx js_simpl.cmx \
     instr.cmx code.cmx primitive.cmx subst.cmx pure_fun.cmx deadcode.cmx \
     flow.cmx inline.cmx \
     tailcall.cmx freevars.cmx phisimpl.cmx \
     linker.cmx generate.cmx parse.cmx main.cmx

compile: $(OBJS:cmx=cmo)
	ocamlfind ocamlc -package findlib,str -linkpkg -g str.cma -o $@ $^

$(COMPILER): $(OBJS)
	ocamlfind ocamlopt -package findlib,str -linkpkg -o $@ $^

%.cmx: %.ml
	ocamlfind ocamlopt -package findlib,str -c $<

%.cmo: %.ml
	ocamlfind ocamlc -package findlib,str -g -c $<

%.cmi: %.mli
	ocamlfind ocamlc -package findlib,str -c $<

clean:
	rm -f *.cm[iox] *.o

depend:
	find . -maxdepth 1 -name private -prune -o -regex ".*\\.mli?" | \
	xargs ocamldep > .depend

include .depend