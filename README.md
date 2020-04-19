
- serve: `docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material`
- deploy: ```sudo docker run --rm -it -v ~/.ssh:/root/.ssh -v `pwd`:/docs squidfunk/mkdocs-material gh-deploy ```
- link: https://armandasrokas.github.io/IntroductionToStatisticsAtDTU/
- docs: https://squidfunk.github.io/mkdocs-material/

