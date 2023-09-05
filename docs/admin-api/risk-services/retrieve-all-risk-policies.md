## Retreive All Risk Policies   

API to retreive all existing risk policies. No path parameter or payload is required.
<!--
type: tab
titles: Request, Response
-->

#### No Payload to Retreive all Policies
<!--
type: tab
-->

### Example of Retreive Risk (201: Created) response

```json
[
    {
        "id": "6bf0f9b0-6ba1-0bbf-0175-4ce7a2dcf2fc",
        "name": "Default Risk Policy",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "3f0c0291-9fba-4481-b670-d56b65a19e83",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 1,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_SCORES",
                    "between": {
                        "minScore": 75,
                        "maxScore": 1000
                    },
                    "aggregatedScores": [
                        {
                            "value": "${details.anonymousNetwork.level}",
                            "score": 50
                        },
                        {
                            "value": "${details.geoVelocity.level}",
                            "score": 50
                        },
                        {
                            "value": "${details.ipRisk.level}",
                            "score": 50
                        },
                        {
                            "value": "${details.userLocationAnomaly.level}",
                            "score": 50
                        },
                        {
                            "value": "${details.ipVelocityByUser.level}",
                            "score": 75
                        },
                        {
                            "value": "${details.newDevice.level}",
                            "score": 75
                        },
                        {
                            "value": "${details.userVelocityByIp.level}",
                            "score": 75
                        },
                        {
                            "value": "${details.userBasedRiskBehavior.level}",
                            "score": 75
                        }
                    ]
                }
            },
            {
                "id": "de670e7b-3623-447d-a093-407011009e29",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 2,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_SCORES",
                    "between": {
                        "minScore": 40,
                        "maxScore": 75
                    },
                    "aggregatedScores": [
                        {
                            "value": "${details.anonymousNetwork.level}",
                            "score": 50
                        },
                        {
                            "value": "${details.geoVelocity.level}",
                            "score": 50
                        },
                        {
                            "value": "${details.ipRisk.level}",
                            "score": 50
                        },
                        {
                            "value": "${details.userLocationAnomaly.level}",
                            "score": 50
                        },
                        {
                            "value": "${details.ipVelocityByUser.level}",
                            "score": 75
                        },
                        {
                            "value": "${details.newDevice.level}",
                            "score": 75
                        },
                        {
                            "value": "${details.userVelocityByIp.level}",
                            "score": 75
                        },
                        {
                            "value": "${details.userBasedRiskBehavior.level}",
                            "score": 75
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            }
        ]
    },
    {
        "id": "09db4854-6650-4608-8c72-04cb9acd09cf",
        "name": "APM00006280810231630_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "b8208761-e933-41bd-9e87-b1a10847aef8",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "b118a987-b00e-417a-b3f3-1916751e2552",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "c2137c8d-aaf5-4cb1-8ca8-4620caa63cd7",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": []
                }
            },
            {
                "id": "5fc5e877-4907-470c-83c8-9f700e48881f",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 0,
                        "maxScore": 50
                    },
                    "aggregatedWeights": []
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            }
        ]
    },
    {
        "id": "1820ed74-666d-40fa-90a2-a5100106c458",
        "name": "APM00006280810231638_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "700fe0b2-3d6c-4da1-96a1-7cea9d372d5d",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "58f8054a-efbe-4390-afcc-96e6b86c0a31",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "bacd4193-91f9-48b2-b699-241d906ad2d8",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 30
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 50
                        }
                    ]
                }
            },
            {
                "id": "5114415d-a0a5-4203-b055-db1d8cdd84cc",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 30
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 50
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "239373cb-2605-4cfb-a16f-257dadb80226",
        "name": "APM00006280810231641_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "3b09273b-52cd-4948-b3db-47edbd276e09",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "4ceddd88-07ac-4002-a96b-54747437bceb",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "0e571a33-ab8b-44b8-a4f3-3cc0858d630d",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "6b1a1325-6eb3-49b0-9a15-682ebefb830d",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "243fefc7-9d14-4928-aa17-9b5e2176eabd",
        "name": "APM0000628081423164718_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "1a010f01-10ae-48f8-a526-9931d492e0b5",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "99f781fb-78e0-4b6d-a6d3-d51dddd2ff71",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "8db6ea9c-9726-4178-b831-703a864a1896",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "3d90c325-657d-4bd4-8cc7-8f389d346a94",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "402aeaa4-ee1f-4aac-a03b-d62307b13dbd",
        "name": "APM0000628081623150815_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "a39f19ce-d33d-4225-8759-3db17a3f60dc",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "aebc9833-0ed3-4278-b959-aeadc067c737",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "a63dc12b-5acc-46f9-ba88-3bc773ed8a87",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "d10ce576-fff8-4fcc-9529-faae4ca4a7ff",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "4fb9a566-4718-4f35-9dad-b16a549b3c5b",
        "name": "APM0000628081423164513_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "fe1f860d-1fbf-439f-9da3-ee682a2f3bd3",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "94861959-8e6c-4e3e-9219-3b11cd56b1f5",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "f29d5d30-7a37-4e22-944c-ea0167c78489",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "0fe319e4-e91f-45eb-b4d3-41df7af557bb",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "5fdb5110-f151-45d2-9af1-fb0cc7c8ed2a",
        "name": "APM0000628081423164108_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "d7713f85-3b98-4e76-b3e6-4c7b92185b4f",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "1f9f3c7c-89ed-49c8-9118-7955c094f72f",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "f4887c44-98e7-4079-8b22-69d42e1d3e8a",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "e1a5cf6a-1103-4458-8778-a5eb8c24915c",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "71e439e7-2c36-4b1a-86d1-1bb34533264f",
        "name": "APM00006280810231637_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "5332227e-c57a-4c42-ac07-21b1e5f7fed5",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "530123d2-e37b-4d32-b956-a5d45d2c54bb",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "6870778e-e62e-494d-8b98-f7259c622e71",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 30
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 50
                        }
                    ]
                }
            },
            {
                "id": "ffac41d9-226e-49ff-8168-615ea3d758f1",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 0,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 30
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 50
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "755b809f-4c97-45c0-a9cd-de61a79a7356",
        "name": "APM00006238_20230822163887_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "787a76b3-f06c-407f-bcc4-2cd6065100aa",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "2be98b3d-a855-400d-b571-9cf9402ebbff",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "b2fe3ad8-1a5e-431c-8be9-4d4bd6c4b6cc",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 7
                        }
                    ]
                }
            },
            {
                "id": "6de8d750-6c22-44ff-8fa9-99ad74a608fd",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 7
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "90044c5d-ae7d-42b9-904e-c5071d6ba133",
        "name": "APM0000628081423164056_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "9e24968a-2df2-4d49-9bc0-34475c13d4ff",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "68abbe54-3608-47fc-90ea-6aa814ab01e9",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "d9ba10e2-d90b-4a14-a0fd-733341cfa2cd",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "ac86b6c3-1ed7-42f4-8f12-fc274e1bc33a",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "a14b4804-63ed-4308-a5f5-b70360befdc4",
        "name": "APM0000628081023180837_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "219ca4bf-4ea1-4bd2-b305-5282b05fd4ed",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "bf0b9988-a4aa-4a1d-b676-f54bcf1a28d5",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "5040a0ff-3c50-4f5e-aed7-b8b23d31276c",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "cf22a32f-8df3-46ed-bbb4-3747c9c09a83",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "a8af87fe-ce45-4ede-9cae-fe0e61f52324",
        "name": "APM0000628081423164130_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "a4949b13-ce38-4689-9782-a539e9fec477",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "dec3865e-1cc7-45b3-b4aa-ad8091a3a900",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "5baf6c69-ec56-4464-95cd-67cb0953eb7b",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "74842840-793d-4757-aafb-d6631d9c25ac",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "c32eb7d1-ae8f-45be-bf4a-a0ff7f2a952e",
        "name": "APM0000628081423164634_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "a7eec23c-82c1-4abb-b3e1-c10a347f9bb8",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "343948f8-5327-437c-aa91-4e3cfb2fd92c",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "51acf38f-1497-4975-86db-cd8d6c81889c",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "d44da240-e9e4-462e-9190-6a047eae0c82",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "da1ef599-3188-4113-acc7-4a6a93a091f8",
        "name": "APM0000628081423164723_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "031870c1-f049-482b-a98b-2a7c8f2d2186",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "9428c698-c079-422d-ba6b-f44dea4180ba",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "02dec448-707f-482b-8260-4419c079e6df",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "2763faf7-c2af-48b0-b14c-d6e3923a7147",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "e35d4ae0-f4ba-4f94-976e-2c84e59504b9",
        "name": "APM0000628081423164446_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "0d26646d-03a6-4e11-8a5e-a2b1537a3314",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "53f71ae9-27bd-4422-8847-43f51f4d9357",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "6c046f44-27b4-42f3-9db4-29358ed4e58b",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "99e66b00-b52a-4c7f-83ae-a94eccb153a5",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "e4fc14c4-9d58-4a9c-9c9d-70a4cbc1cca7",
        "name": "APM0000628081623151436_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "af0c2e86-6178-49d6-b9ac-0d8be9ed72cf",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "545a9eec-36c4-424b-8139-a0f6da3d9d47",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "9aadfab4-bae6-4b55-9864-543afb3e3914",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "fb682a67-aa3f-4680-8dd0-efdea7f03eaf",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "eff6bf38-fef1-4d2a-b423-6a4e13d5b2ed",
        "name": "APM00006238_20230822163228_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "e6b1462a-a627-4f9a-bad6-829a178c4c43",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "fd69f2e0-f9d2-414f-9802-3f3e6a481dda",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "5686a08c-221e-4bd9-b712-4b00a87e3efc",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "6f2d9ee0-a216-4fc3-8c0c-6c91cb7ad7b8",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 30,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "f6cea8bc-5942-4a32-9b6a-4ed126eb1dd8",
        "name": "APM000062832210231601_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [
            {
                "id": "772d29e6-73bb-405b-9b15-8b8fbc9ea52a",
                "name": "ANONYMOUS_NETWORK_DETECTION",
                "priority": 1,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.anonymousNetwork.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "7ff1104a-2a6b-4315-907b-16a4946a7016",
                "name": "GEOVELOCITY_ANOMALY",
                "priority": 2,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "value": "${details.geoVelocity.level}",
                    "equals": "HIGH",
                    "type": "VALUE_COMPARISON"
                }
            },
            {
                "id": "910a3577-99fc-4482-a627-d0f343d4f499",
                "name": "HIGH_WEIGHTED_POLICY",
                "priority": 3,
                "result": {
                    "level": "HIGH",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 50,
                        "maxScore": 100
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            },
            {
                "id": "68fda5d7-590d-4cce-88fa-0d694db2c2fd",
                "name": "MEDIUM_WEIGHTED_POLICY",
                "priority": 4,
                "result": {
                    "level": "MEDIUM",
                    "type": "VALUE"
                },
                "condition": {
                    "type": "AGGREGATED_WEIGHTS",
                    "between": {
                        "minScore": 40,
                        "maxScore": 50
                    },
                    "aggregatedWeights": [
                        {
                            "value": "${details.aggregatedWeights.userRiskBehavior}",
                            "weight": 3
                        },
                        {
                            "value": "${details.aggregatedWeights.ipVelocityByUser}",
                            "weight": 5
                        }
                    ]
                }
            }
        ],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            },
            {
                "id": "2e2576f1-7cb0-09ec-0601-8b56e55ecde7"
            }
        ]
    },
    {
        "id": "fd4ca0cb-8a43-4035-8e44-b05dc6d382b8",
        "name": "AppID1_RISK_POLICY",
        "defaultResult": {
            "level": "LOW",
            "type": "VALUE"
        },
        "riskPolicies": [],
        "evaluatedPredictors": [
            {
                "id": "73707b17-8476-0dca-2bfb-4769049b113d"
            },
            {
                "id": "32eb6e4b-1b16-0534-1d05-787b6dd20014"
            },
            {
                "id": "6f6166d1-a133-0131-30f9-b43bf322539e"
            },
            {
                "id": "2cb4bfd5-c55e-02e9-165c-0f25b9b68973"
            },
            {
                "id": "823f486b-3c9f-02b1-05b6-8aa2400985ad"
            },
            {
                "id": "5bf21394-aa62-0ea3-2f2b-1993ed0e55c8"
            },
            {
                "id": "8a46dbcd-844a-0243-3131-086b3b54b02e"
            },
            {
                "id": "f5ad414d-7897-0d90-2e83-4a816abd19eb"
            }
        ]
    }
]
```
<!-- type: tab-end -->