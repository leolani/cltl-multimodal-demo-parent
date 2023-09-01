SHELL = /bin/bash

project_dependencies ?= $(addprefix $(project_root)/, \
		emissor \
		cltl-combot \
		cltl-requirements \
		cltl-backend \
		cltl-face-recognition \
		cltl-object-recognition \
		cltl-emissor-data \
		cltl-emotionrecognition \
		cltl-knowledgerepresentation \
		cltl-knowledgeextraction \
		cltl-knowledgelinking \
		cltl-languagegeneration \
		cltl-mention-detection \
		cltl-g2ky \
		cltl-leolani \
		cltl-chat-ui)

git_remote ?= https://github.com/leolani

sources =

include util/make/makefile.base.mk
include util/make/makefile.py.base.mk
include util/make/makefile.git.mk
include makefile.helm.mk


spacy.lock: venv
	test -e spacy.lock || (source venv/bin/activate; python -m spacy download en)
	touch spacy.lock


nltk.lock: venv
	test -e nltk.lock || (source venv/bin/activate; python -m nltk.downloader -d ~/nltk_data all)
	touch nltk.lock


py-app/resources/conversational_triples/models.lock:
	mkdir -p py-app/resources/conversational_triples
	wget "https://vu.data.surfsara.nl/index.php/s/WpL1vFChlQpkbqW/download" -O py-app/resources/conversational_triples/models.zip
	unzip -j -d py-app/resources/conversational_triples py-app/resources/conversational_triples/models.zip
	rm py-app/resources/conversational_triples/models.zip
	touch py-app/resources/conversational_triples/models.lock


.PHONY: build
build: venv \
    nltk.lock spacy.lock \
    py-app/resources/conversational_triples/models.lock


.PHONY: clean
clean: py-clean base-clean
	rm -f spacy.lock nltk.lock
	rm -rf py-app/resources/conversational_triples
