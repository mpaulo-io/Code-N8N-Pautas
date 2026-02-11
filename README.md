{
  "nodes": [
    {
      "parameters": {
        "amount": 10
      },
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        1184,
        -32
      ],
      "id": "d1ec5626-a256-42c8-974e-459fe7b345f6",
      "name": "Descanso Anti-Bloqueio (15s)",
      "webhookId": "083c1db6-2c9c-4dcb-a204-a20495d77793"
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1aRWrw6TQtgRW4jtLvmXJIyJQ7DmPcD2eeyAnpZGFE6o",
          "mode": "list",
          "cachedResultName": "Estrutura da Planilha",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1aRWrw6TQtgRW4jtLvmXJIyJQ7DmPcD2eeyAnpZGFE6o/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "📝 Fila de Postagem",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1aRWrw6TQtgRW4jtLvmXJIyJQ7DmPcD2eeyAnpZGFE6o/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Tema": "={{ $json.Tema }}",
            "Palavra-Chave": "={{ $json['Palavra-Chave'] }}",
            "Categoria": "={{ $json.Categoria }}",
            "Persona": "={{ $json.Persona }}",
            "Status": "={{ $json.Status }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "ID",
              "displayName": "ID",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Tema",
              "displayName": "Tema",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Palavra-Chave",
              "displayName": "Palavra-Chave",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Categoria",
              "displayName": "Categoria",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Persona",
              "displayName": "Persona",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Status",
              "displayName": "Status",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "URL Final",
              "displayName": "URL Final",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Data de Publicação",
              "displayName": "Data de Publicação",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        1216,
        160
      ],
      "id": "b22e0632-c3b9-4f24-a046-0c0e06c466ab",
      "name": "Salvar Ideias na Fila de Postagem",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "HpaJQgK9yT8xa4Kh",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "url": "https://trends.google.com/trending/rss?geo=BR",
        "options": {}
      },
      "type": "n8n-nodes-base.rssFeedRead",
      "typeVersion": 1.2,
      "position": [
        352,
        80
      ],
      "id": "e1c885cb-ae5a-48c4-9c1d-1d4e761f3c41",
      "name": "Buscar Trends Google BR (RSS)"
    },
    {
      "parameters": {
        "maxItems": 3
      },
      "type": "n8n-nodes-base.limit",
      "typeVersion": 1,
      "position": [
        496,
        -96
      ],
      "id": "315576cd-56dc-44ee-a4dd-6f12f82ae59b",
      "name": "Selecionar Top 3 Trends"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 3,
      "position": [
        992,
        -96
      ],
      "id": "098ec359-909b-4296-be12-e4e6abc78a2e",
      "name": "Processar 1 a 1 (Loop)"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={\n  \"agent_identity\": {\n    \"role\": \"Chief Digital Architect - Nicho Educação Bilíngue\",\n    \"seniority\": \"Sênior / Estrategista de Growth\",\n    \"philosophy\": \"Value-Based Authority (VDA): O conteúdo deve ser tão valioso que o usuário pagaria por ele. A conversão é a consequência ética da confiança estabelecida.\",\n    \"compliance_2026\": [\"E-E-A-T High-Level\", \"Privacy-First Data\", \"Anti-Burnout Content (Qualidade > Volume)\"]\n  },\n\n  \"validation_logic\": {\n    \"sanity_check\": \"Rejeitar tendências de baixo ROI ou 'vanity metrics'. Se o tema não constrói autoridade de longo prazo, ativar FALLBACK_STRATEGIC_ASSET.\",\n    \"competitor_filter\": \"O conteúdo deve ser impossível de ser replicado por uma IA genérica sem dados proprietários (Zero-Party Data).\"\n  },\n\n  \"strategic_pillars\": {\n    \"pilar_1_tech_efficiency\": \"Otimização para Search Generative Experience (SGE). Uso de dados estruturados e linguagem natural para 'Agents-to-Agents' (A2A).\",\n    \"pilar_2_human_management\": \"Foco na jornada emocional dos pais (alívio de carga cognitiva). Conteúdo que educa sem gerar burnout parental.\",\n    \"pilar_3_profitability\": \"Foco em LTV e CAC reverso. Cada peça de conteúdo deve servir como entrada para um funil de retenção, não apenas uma venda única.\"\n  },\n\n  \"decision_engine_3d\": {\n    \"axis_x_viral\": \"Score 0-10 (Potencial de compartilhamento orgânico/emocional)\",\n    \"axis_y_commercial\": \"Score 0-10 (Alinhamento com produtos de alta margem)\",\n    \"axis_z_authority\": \"Score 0-10 (Quanto isso posiciona a marca como líder de pensamento)\",\n    \"action_matrix\": {\n      \"High_All\": \"Master Asset: Vídeo Longo (YouTube/Course) + Reel + Artigo Pillar + Newsletter\",\n      \"High_Viral_Low_Comm\": \"Lead Magnet: Conteúdo topo de funil para captura de e-mail/WhatsApp\",\n      \"Low_Viral_High_Comm\": \"Sniper Sale: Artigo de comparação técnica (Bottom of Funnel) focado em SEO transacional\",\n      \"Fallback\": \"Evergreen Education: Reforço de marca com base em 'Dores de Rotina' reais.\"\n    }\n  },\n\n  \"execution_framework_eeat\": {\n    \"personal_evidence_protocol\": \"Obrigatório: Relato em 1ª pessoa com 'imperfeições humanizantes' (ex: 'Tentei o método X, mas na terça-feira foi um caos porque...').\",\n    \"technical_depth\": \"Incluir 1 insight de neurociência ou pedagogia aplicada (ex: Janela de Plasticidade Cerebral 0-3 anos).\",\n    \"ethical_sales\": \"Substituir gatilhos de escassez falsa por 'Gatilhos de Facilitação' (ex: 'Este recurso economiza 2h da sua semana de planejamento').\"\n  },\n\n  \"output_architecture_json\": {\n    \"instruction\": \"RESPONDA APENAS JSON. ZERO PROSE.\",\n    \"schema\": {\n      \"strategic_diagnosis\": {\n        \"market_gap\": \"Por que este conteúdo é necessário agora?\",\n        \"target_persona_stage\": \"Consciência do Problema | Solução | Produto\",\n        \"scores\": { \"viral\": 0, \"commercial\": 0, \"authority\": 0 }\n      },\n      \"content_blueprint\": {\n        \"title_h1\": \"Título Magnético (SEO + Click-through)\",\n        \"format_ecosystem\": [\"Lista de canais\"],\n        \"educational_core_70\": \"Resumo do valor entregue antes do pitch\",\n        \"conversion_bridge_30\": \"Como o produto se torna a solução natural\",\n        \"human_touch_evidence\": \"O relato real simulado/extraído\"\n      },\n      \"business_metrics_estimated\": {\n        \"primary_kpi\": \"Ex: CTR, Conversão, Retenção\",\n        \"estimated_roi_tier\": \"Baixo | Médio | Alto\",\n        \"next_step_cta\": \"Ação estratégica recomendada\"\n      }\n    }\n  },\n\n  \"workflow\": \"1. Validar input contra filtros de sanidade. 2. Calcular Matriz 3D. 3. Aplicar Protocolo EEAT. 4. Estruturar Ecossistema de Conteúdo. 5. Gerar Output JSON.\"\n}",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3.1,
      "position": [
        800,
        144
      ],
      "id": "7a7730ec-d0b5-4ad0-8516-b4c3bd9e6f10",
      "name": "Analisar & Gerar Pauta (Gemini)"
    },
    {
      "parameters": {
        "jsCode": "// ============================================\n// PARSER ULTRA-ROBUSTO DE JSON DO GEMINI\n// ============================================\n\n// 1. CAPTURA SEGURA DO OUTPUT\nlet raw = '';\ntry {\n  // Tenta múltiplas fontes de dados\n  const item = $input.item.json;\n  raw = item.output || item.text || item.response || '';\n  \n  // Se veio array, pega primeiro item\n  if (Array.isArray(raw)) {\n    raw = raw[0];\n  }\n  \n  // Converte objetos para string\n  if (typeof raw === 'object') {\n    raw = JSON.stringify(raw);\n  }\n  \n  raw = String(raw).trim();\n  \n  if (!raw) {\n    throw new Error('Output vazio do Gemini');\n  }\n} catch (e) {\n  console.error('❌ Erro ao capturar output:', e.message);\n  raw = '{}';\n}\n\n// 2. LIMPEZA AGRESSIVA\nfunction cleanJSON(text) {\n  return text\n    .replace(/```(?:json)?/gi, '')           // Remove markdown\n    .replace(/```/g, '')                     // Remove blocos\n    .replace(/^[^{]*(\\{[\\s\\S]*\\})[^}]*$/, '$1') // Extrai apenas JSON\n    .replace(/[\\r\\n\\t]+/g, ' ')              // Normaliza espaços\n    .replace(/,(\\s*[}\\]])/g, '$1')           // Remove vírgulas trailing\n    .trim();\n}\n\n// 3. PARSE COM FALLBACK INTELIGENTE\nlet data;\ntry {\n  const cleaned = cleanJSON(raw);\n  \n  if (!cleaned || cleaned === '{}') {\n    throw new Error('JSON vazio após limpeza');\n  }\n  \n  data = JSON.parse(cleaned);\n  \n  // Valida campos obrigatórios\n  if (!data.tema || !data.palavra_chave) {\n    throw new Error('Campos obrigatórios faltando');\n  }\n  \n} catch (e) {\n  console.error('❌ Erro ao parsear JSON:', {\n    error: e.message,\n    rawPreview: raw.substring(0, 150) + '...',\n    cleaned: cleanJSON(raw).substring(0, 150) + '...'\n  });\n  \n  // FALLBACK: Cria conteúdo evergreen de emergência\n  const evergreenTopics = [\n    {\n      tema: \"10 Músicas em Inglês para Bebês Dormirem Tranquilos\",\n      palavra_chave: \"músicas inglês bebês dormir\",\n      persona: \"Bebês\",\n      categoria: \"Músicas\"\n    },\n    {\n      tema: \"Como Ensinar Cores em Inglês: 15 Brincadeiras Divertidas\",\n      palavra_chave: \"ensinar cores inglês crianças\",\n      persona: \"Crianças 3-6\",\n      categoria: \"Jogos\"\n    },\n    {\n      tema: \"Rotina Matinal em Inglês: Frases para Usar Todo Dia\",\n      palavra_chave: \"rotina matinal inglês crianças\",\n      persona: \"Pais\",\n      categoria: \"Rotina\"\n    }\n  ];\n  \n  // Escolhe um aleatório\n  data = evergreenTopics[Math.floor(Math.random() * evergreenTopics.length)];\n  data.relevante = false;\n  data.erro_parse = true;\n}\n\n// 4. VALIDAÇÃO E NORMALIZAÇÃO\nconst personasValidas = [\"Bebês\", \"Crianças 3-6\", \"Alfabetização\", \"Pais\", \"Geral\"];\nconst categoriasValidas = [\"Rotina\", \"Músicas\", \"Jogos\", \"Filmes\", \"Dicas Diárias\", \"Evergreen\"];\n\n// Garante valores válidos\nif (!personasValidas.includes(data.persona)) {\n  data.persona = \"Geral\";\n}\n\nif (!categoriasValidas.includes(data.categoria)) {\n  data.categoria = \"Evergreen\";\n}\n\n// Limpa e valida palavra-chave\ndata.palavra_chave = String(data.palavra_chave)\n  .toLowerCase()\n  .replace(/[^a-záàâãéêíóôõúç\\s-]/gi, '')\n  .trim();\n\n// Limita tamanho do tema\nif (data.tema.length > 80) {\n  data.tema = data.tema.substring(0, 77) + '...';\n}\n\n// 5. RETORNO PADRONIZADO PARA GOOGLE SHEETS\nreturn {\n  json: {\n    Tema: data.tema,\n    \"Palavra-Chave\": data.palavra_chave,\n    Categoria: data.categoria,\n    Persona: data.persona,\n    Status: \"Pendente\",\n    \"Origem Trend\": data.relevante !== false ? \"Trend Adaptado\" : \"Evergreen\",\n    \"Data Captura\": new Date().toISOString().split('T')[0],\n    \"Erro Parse\": data.erro_parse || false\n  }\n};"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1344,
        -32
      ],
      "id": "7bc9d7eb-f174-448d-856f-96225792d831",
      "name": "Limpar JSON do Gemini"
    },
    {
      "parameters": {
        "rule": {
          "interval": [
            {}
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.3,
      "position": [
        128,
        80
      ],
      "id": "167d50db-8990-4915-be74-5a8127ff21ec",
      "name": "Agendar Busca Noturna"
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "value": "gpt-4.1-mini",
          "mode": "list",
          "cachedResultName": "gpt-4.1-mini"
        },
        "builtInTools": {},
        "options": {
          "maxTokens": 1500,
          "temperature": 0.5
        }
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.3,
      "position": [
        480,
        304
      ],
      "id": "e2162a4b-e6c5-432a-a16f-049b808f80d5",
      "name": "OpenAI Chat Model",
      "credentials": {
        "openAiApi": {
          "id": "HYk4F9hj3pcSEz0z",
          "name": "OpenAi account 2"
        }
      }
    },
    {
      "parameters": {
        "model": "llama-3.3-70b-versatile",
        "options": {
          "maxTokensToSample": 3500,
          "temperature": 0.4
        }
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGroq",
      "typeVersion": 1,
      "position": [
        784,
        304
      ],
      "id": "f1bdaf39-69bf-487d-a61d-bbd0907809c5",
      "name": "Groq Chat Model",
      "credentials": {
        "groqApi": {
          "id": "TC3xIKHI5WiphGZ7",
          "name": "Groq account 2"
        }
      }
    }
  ],
  "connections": {
    "Descanso Anti-Bloqueio (15s)": {
      "main": [
        [
          {
            "node": "Limpar JSON do Gemini",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Salvar Ideias na Fila de Postagem": {
      "main": [
        [
          {
            "node": "Processar 1 a 1 (Loop)",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Buscar Trends Google BR (RSS)": {
      "main": [
        [
          {
            "node": "Selecionar Top 3 Trends",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Selecionar Top 3 Trends": {
      "main": [
        []
      ]
    },
    "Processar 1 a 1 (Loop)": {
      "main": [
        [],
        [
          {
            "node": "Analisar & Gerar Pauta (Gemini)",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Analisar & Gerar Pauta (Gemini)": {
      "main": [
        [
          {
            "node": "Descanso Anti-Bloqueio (15s)",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Limpar JSON do Gemini": {
      "main": [
        [
          {
            "node": "Salvar Ideias na Fila de Postagem",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Agendar Busca Noturna": {
      "main": [
        [
          {
            "node": "Buscar Trends Google BR (RSS)",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [
        []
      ]
    },
    "Groq Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "Analisar & Gerar Pauta (Gemini)",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    }
  },
  "pinData": {},
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "15e5e4d98fce5be652f67c4482f3751ad200fedbc3d8da2c3a64063a7f1f5f49"
  }
}
