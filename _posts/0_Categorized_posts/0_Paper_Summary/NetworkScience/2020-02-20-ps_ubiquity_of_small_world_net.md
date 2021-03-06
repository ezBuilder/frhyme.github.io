---
title: PaperSummary - The Ubiquity of Small-World Networks
category: paper-summary
tags: paper-summary small-world network latticization graph-theory
---

## 2-line summary 

- 이 논문 이전에는 random network만을 reference로 삼아, small-world network를 결정하였으나, 정확하지 못했음. 
- 여기서는 lattice network, random network를 함께 비교하여, small-world 를 더 잘 판별해주는 `omega`를 제시하였음.

## The Ubiquity of Small-World Networks

- 최근에, network의 small-worldness를 정리하고 있습니다. 보통 small-worldness는 "clustering coefficient가 특별히 높고, average shortest path length가 특별하 낮다"라는 성질을 공유하죠. 
- 그리고, 이 때, 이 "특별함"을 판단하는 기준으로서 두가지 network를 사용하게 됩니다. 하나는, 그냥 random network(degree를 똑같이 유지하고, edge를 교환하면서 생성), 그리고 두번째는 lattice network죠. 
- 아쉽게도, lattice network는 정확하게 정리된 것이 없습니다. 그래서 계속 찾아보다가, 이 논문 속에서 그나마 좀 정리되어 있는 것을 발견했죠. 
- 해당 논문은 2011년에 게재되었으며, [여기에서](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3604768/) 읽을 수 있습니다.

## Abstract 번역

- Watts 와 Strogatz에 따르면, `Small-world network`는 network의 한 종류로서, "regular lattice처럼 특별히 군집화되고(highly clustered), 하지만, random network 처럼 특별히 작은 average shortest path lengh를 가진다"라는 특징을 가집니다. 
- 이와 같은 특성은 효율적인 정보 전송(efficient information transfer)를 위한 지역적 특성화(regional specialization)이라는 특이한 성질을 네트워크에 부여하죠. 
- Social network가 small network의 한 예로서, 사람들은 친구들과 다양한 그룹들(clique or cluster)을 가지고 있지만, 그러함에도 어떤 사람들과 단지 6단계만으로 도달가능하죠. 
- 비록, 이미 네트워크 과학 분야에서, 이와 같은 정량적인 정의가 충분히 진행되었지만(have prevailed), 실용적인 관점에서(in application)는 사실, 그냥 random network만을 기준으로 두고, average path length(대안적인 분산 처리 지표), clustering(대안적인 지역적 특성화(regional specializtion) 측정 지표)를 비교하고 있다. 하지만, 단지 random network만을 기준으로 두고, clustering을 비교하는 것은 이미 small-world 성질을 보여주기 위해서 어려운 부분이 있다는 것이 드러났다. 
- 따라서, 우리는 새로운 small-world metric인 `omega`를 제시하며, 이를 통해, lattice network, random network를 함께 비교하여, small-world를 더 정확하게 측정하려고 한다.
- 예시로 사용한 network에서, 그저, clustering을 사용하여, random network와 비교하였을 때는 small-world로 해석되었으나, `omega`를 사요하여 비교했을 때는 small-world가 아닌 것으로 드러났다.
- small-world network 특별한 위상학적인 성질(unique topological properties)을 갖추고 있기 때문에, 이와 같은 발견은 네트워크 과학 분야에서 특별한 의미를 가지며(important implication), 그저 "높은 clustering과 짧은 최단거리"를 가지고 있는 네트워크 들 중에서, small-world 네트워크를 더 정확하게 판단할 수 있을 것이다.


## lattice network construction. 

- 사실, 이 부분이 제일 보고 싶었던 것이었죠. `networkx.lattice_refernce`에서는 `D`라는 "distance to diagonal matrix"를 기본으로 사용하여 계산합니다. 미묘하게 이해가 잘 되지는 않더군요. 왜 그래야 하는지. 
- 본 논문에서는 위에 대한 내용도 있지만, 오히려, 아래의 내용이 저에게는 더 친숙하게 느껴집니다.

> Storing the initial adjacency matrix and its clustering coefficient, the latticization procedure is performed on the matrix. If the clustering coefficient of the resulting matrix is lower, the initial matrix is kept and latticization is performed again on the same matrix; if the clustering coefficient is higher, then the initial adjacency matrix is replaced. This latticization process is repeated until clustering is maximized. This process results in a highly clustered network with long path length approximating a lattice topology.

- 요약하자면, 처음에 adjancency matrix와 clustering coefficient를 저장해두고, clustering coefficient가 커지면, 변형하고, 아니면 되돌려라. 즉, greedy하게 탐색하라는 말이겠죠. 
- lattice network를 가져오는 이유는, 사실 degree sequence가 같을 때, 가장 clustering이 높고, 반대로 average shortest path length의 길이가 높은 네트워크이기 때문인 것이죠.
- 따라서, 어떤 방법이든, clustering을 최대로 높이는 network를 찾으면 장땡이 아닐까 싶습니다.