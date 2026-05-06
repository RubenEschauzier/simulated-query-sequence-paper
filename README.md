The easily reproducible experiments required to obtain the results in this paper are found here:
https://github.com/RubenEschauzier/experiments-link-traversal-caching-random-query-sequences.
Each experiment has an easy to follow README.md requiring very little setup.

Within this repository the following branches are used in the paper:
- experiment/cache - The experiments associated with **Unindexed Cache**, running this experiment
will produce the data for all three cache sizes
- experiment/query-cache - The experiments associated with **Indexed Cache**, running this experiment
will produce the data for all three cache sizes
- experiment/query-cache-estimate - The experiments associated with **Indexed Cache + Cardinality estimation**, running this experiment
will produce the data for all three cache sizes.
- experiment/synthetic-cache-hitrate - The experiments ran to get the synthetic hitrate data for the **Unindexed Cache**.
- experiment/synthetic-query-cache-hitrate - The experiments ran to get the synthetic hitrate data for the **Indexed Cache**.

For the experiments using random query sequences the experiments are found here:
https://github.com/RubenEschauzier/experiments-link-traversal-caching-random-query-sequences.

Within the repository we have the following branches, similar to the other experiment repo:
- experiment/cache - The experiments associated with **Unindexed Cache**, running this experiment
will produce the data for all three cache sizes
- experiment/query-cache - The experiments associated with **Indexed Cache**, running this experiment
will produce the data for all three cache sizes
- experiment/query-cache-estimate - The experiments associated with **Indexed Cache + Cardinality estimation**, running this experiment
will produce the data for all three cache sizes.

The raw data produced by these experiments is found on Zenodo: \url{https://zenodo.org/records/20056413}.
We use this python repository to process this data and generate the figures and tables from the paper: https://github.com/RubenEschauzier/process-raw-caching-jbr-output.


The source code and documentation for the different code bases updated to create SolidSessionBench are:
-  The LDBC-SNB enhancer: Updated to generate similarity data between users and users and their posts. Documentation and source code is available:
https://github.com/SolidBench/ldbc-snb-enhancer.js#similarity-configuration. 
- The rdf-dataset-fragmenter: Updated to allow the rdf-dataset-fragmenter to output the original and transformed terms within a quad.
This allows us to map a fragmented query string (with transformed NamedNodes) to a query which we can execute over the original SNB dataset.
Documentation and code are available here: https://github.com/SolidBench/rdf-dataset-fragmenter.js#transform-callbacks
- The sparql-query-parameter-instantiator: The main updated codebase, Here we've added the complex query sequence generation logic, supported
by the functionalities added in the other repositories. (TODO: Explain briefly what this does)
Documentation and code are available here: https://github.com/SolidBench/sparql-query-parameter-instantiator.js#query-sequence-instantiator
- SolidBench.js: The centralized repository integrated all changes. This is updated to include sensible default configurations which are also used
for all experiments in the paper.
Documentation and code are available here: https://github.com/SolidBench/SolidBench.js

Finally the source code for the caching implementations is located here:
https://github.com/RubenEschauzier/comunica-feature-link-traversal/tree/feature/http-caching-adaptive-join
Which requires an updated version of Comunica, located here:
https://github.com/RubenEschauzier/comunica/tree/feature/caching-adaptive-join

To run these locally, you need to follow the official Comunica documentation here: https://comunica.dev/docs/modify/advanced/linking_local_version/#yarn-workspaces
The docker image used in all experiments is `rubeneschauzier/comunica-feature-link-traversal-caching:dev`.
The index digest for the experiment version is: `sha256:9cacaab6409ec5abd289675ff5db83b08508cfc407c51bac4ef8de2b2bb711c8`.
