## Query

```sparql
prefix ibbeo: <https://ontologies.industrybuildingblocks.com/ibbeo/>
prefix ibbeox: <https://taxonomies.industrybuildingblocks.com/ibbeo/>
prefix ibbeod: <https://data.industrybuildingblocks.com/ibbeo/>
prefix skos: <http://www.w3.org/2004/02/skos/core#>
prefix gist: <https://ontologies.semanticarts.com/gist/>
prefix xsd: <http://www.w3.org/2001/XMLSchema#>

construct {
  ?topOrgSub ?topOrgPred ?topOrgObj .
  ?childOrgSub ?childOrgPred ?childOrdObj .
}
where {
  values ?topOrgSub {
    <https://data.industrybuildingblocks.com/ibbeo/_Organization_1075339>
  }
  {
    ?topOrgSub
      rdf:type ibbeo:IbbOrganization ;
      gist:isCategorizedBy ibbeox:_OrganizationLevel_TopParent ;
      ?topOrgPred ?topOrgObj ;
    .
    FILTER (
      ?topOrgPred IN (
        skos:prefLabel,
        ibbeo:primaryMarketBrandName
      )
    )
  }
  union
  {
    ?childOrgSub
      rdf:type ibbeo:IbbOrganization ;
      ibbeo:hasImmediateParent+ ?topOrgSub ;
      ?childOrgPred ?childOrdObj ;
    .
    FILTER (
      ?childOrgPred IN (
        skos:prefLabel,
        ibbeo:primaryMarketBrandName,
        ibbeo:hasImmediateParent
      )
    )
  }
}
order by ?topOrgSub ?topOrgPred ?childOrgSub ?childOrgPred
```

## Raw Input

Note: Duplicate cases were commented out to help simplify the diagram. See the raw mermaid text for complete graph.

```mermaid
graph TD
    A[Morningstar] -->|pmbn| a[Morningstar]
    A[Morningstar] -->|pmbn| ALegalName[Morningstar, Inc]

    B[PitchBook Workflow Tools] -->|iParent| A
    B -->|pmbn| b[PitchBook]

    %% Duplicate test case
    %% C[PitchBook Services] -->|iParent| A
    %% C -->|pmbn| b

    D[PitchBook Data Inc] -->|iParent| A
    D -->|pmbn| d[PitchBook Data]

    %% Duplicate test case
    %% E[Morningstart Investment Services Inc] -->|iParent| A
    %% E -->|pmbn| e[Morningstart Investment Services]

    F[Morningstar Associates LLC] -->|iParent| A
    F -->|pmbn| f[Morningstar Associates]

    G[Hemscott data] -->|iParent| A
    G -->|pmbn| g[Hemscott data]

    %% Duplicate test case
    %% H[PitchBook Private Equity & Venture Capital Data] -->|iParent| D
    %% H -->|pmbn| b

    %% Duplicate test case
    %% I[PitchBook Platform] -->|iParent| D
    %% I -->|pmbn| b

    %% Duplicate test case
    %% J[PitchBook PB Mobile App] -->|iParent| D
    %% J -->|pmbn| b

    K[PitchBook Data] -->|iParent| D
    K -->|pmbn| b

    %% Duplicate test case
    %% L[PitchBook API & Datafeed] -->|iParent| D
    %% L -->|pmbn| b

    M[PitchBook People Data] -->|iParent| K
    M -->|pmbn| b

    %% Duplicate test case
    %% N[PitchBook News & Analysis] -->|iParent| K
    %% N -->|pmbn| b

    %% Duplicate test case
    %% O[PitchBook M&A Data] -->|iParent| K
    %% O -->|pmbn| b

    %% Duplicate test case
    %% P[PitchBook Limited Partner Data] -->|iParent| K
    %% P -->|pmbn| b

    %% Duplicate test case
    %% Q[PitchBook Investor Data] -->|iParent| K
    %% Q -->|pmbn| b

    %% Duplicate test case
    %% R[PitchBook Fund Data] -->|iParent| K
    %% R -->|pmbn| b

    %% Duplicate test case
    %% S[PitchBook Deal Data] -->|iParent| K
    %% S -->|pmbn| b

    %% Duplicate test case
    %% T[PitchBook Company Data] -->|iParent| K
    %% T -->|pmbn| b

    %% Duplicate test case
    %% U[PitchBook Advisor Data] -->|iParent| K
    %% U -->|pmbn| b

    %% V[Foobar] -->|iParent| K
    %% V -->|pmbn| z[Foo]

    %% Z[Foobar] -->|iParent| K
    %% Z -->|pmbn| z[Foo]
```

## Desired Brand Hierarchy


Note: Duplicate cases were commented out to help simplify the diagram. See the raw mermaid text for complete graph.

```mermaid
graph TD
    TP[Morningstar] -->|legalName| TPLegalName[Morningstar, Inc]

    a[Morningstar] -->|hasCompany| TP

    b[PitchBook] -->|iParent| a

    B[PitchBook Workflow Tools] -->|iParent| b
    %% B|pmbn| b[PitchBook] -->

    %% Duplicate test case
    C[PitchBook Services] -->|iParent| b
    %% C -->|pmbn| b

    D[PitchBook Data Inc] -->|iParent| K
    %% D -->|pmbn| d[PitchBook Data]

    %% Duplicate test case
    %% E[Morningstart Investment Services Inc] -->|iParent| a
    %% E -->|pmbn| e[Morningstart Investment Services]

    F[Morningstar Associates LLC] -->|iParent| f
    %% F -->|pmbn| f[Morningstar Associates]

    f[Morningstar Associates] -->|iParent| a

    G[Hemscott data] -->|iParent| a
    %% G -->|pmbn| g[Hemscott data]

    %% Duplicate test case
    %% H[PitchBook Private Equity & Venture Capital Data] -->|iParent| D
    %% H -->|pmbn| b

    %% Duplicate test case
    %% I[PitchBook Platform] -->|iParent| D
    %% I -->|pmbn| b

    %% Duplicate test case
    %% J[PitchBook PB Mobile App] -->|iParent| D
    %% J -->|pmbn| b

    K[PitchBook Data] -->|iParent| b
    %% K -->|pmbn| b

    %% Duplicate test case
    %% L[PitchBook API & Datafeed] -->|iParent| D
    %% L -->|pmbn| b

    M[PitchBook People Data] -->|iParent| K
    %% M -->|pmbn| b

    %% Duplicate test case
    %% N[PitchBook News & Analysis] -->|iParent| K
    %% N -->|pmbn| b

    %% Duplicate test case
    %% O[PitchBook M&A Data] -->|iParent| K
    %% O -->|pmbn| b

    %% Duplicate test case
    %% P[PitchBook Limited Partner Data] -->|iParent| K
    %% P -->|pmbn| b

    %% Duplicate test case
    %% Q[PitchBook Investor Data] -->|iParent| K
    %% Q -->|pmbn| b

    %% Duplicate test case
    %% R[PitchBook Fund Data] -->|iParent| K
    %% R -->|pmbn| b

    %% Duplicate test case
    %% S[PitchBook Deal Data] -->|iParent| K
    %% S -->|pmbn| b

    %% Duplicate test case
    %% T[PitchBook Company Data] -->|iParent| K
    %% T -->|pmbn| b

    %% Duplicate test case
    %% U[PitchBook Advisor Data] -->|iParent| K
    %% U -->|pmbn| b

    %% V[Foobar] -->|iParent| K
    %% V -->|pmbn| z[Foo]

    %% Z[Foobar] -->|iParent| K
    %% Z -->|pmbn| z[Foo]
```
