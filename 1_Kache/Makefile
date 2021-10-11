DOT = dot

DOTFILES = basic_concepts.svg basic_concepts_without_homesvr.svg \
	fedi_arch.svg
DOTSVGFLAGS := -Tsvg

all: images

images: $(DOTFILES)

%.svg: %.dot
	$(DOT) $(DOTSVGFLAGS) -o$@ $<
