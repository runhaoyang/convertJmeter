const fs = require("fs");
const builder = require("xmlbuilder");
let fileName = "testPlan.jmx";

// Function to create the TestPlan
const createTestPlan = (rootHashTree) => {
  const testPlan = rootHashTree.ele("TestPlan", {
    guiclass: "TestPlanGui",
    testclass: "TestPlan",
    testname: "Test plan name",
  });

  testPlan
    .ele("elementProp", {
      name: "TestPlan.user_defined_variables",
      elementType: "Arguments",
      guiclass: "ArgumentsPanel",
      testclass: "Arguments",
    })
    .ele("collectionProp", { name: "Arguments.arguments" });

  return rootHashTree;
};

// Function to create Arguments element (User Defined Variables)
const createUserDefinedVariables = (rootHashTree) => {
  const userDefinedVariables = rootHashTree.ele("Arguments", {
    guiclass: "ArgumentsPanel",
    testclass: "Arguments",
    testname: "User Defined Variables",
  });

  userDefinedVariables.ele("collectionProp", { name: "Arguments.arguments" });

  return rootHashTree;
};

// Function to create CookieManager element
const createCookieManager = (rootHashTree) => {
  const cookieManager = rootHashTree.ele("CookieManager", {
    guiclass: "CookiePanel",
    testclass: "CookieManager",
    testname: "HTTP Cookie Manager",
  });

  cookieManager.ele("collectionProp", { name: "CookieManager.cookies" });
  cookieManager.ele("boolProp", { name: "CookieManager.clearEachIteration" }).txt("true");
  cookieManager.ele("boolProp", { name: "CookieManager.controlledByThreadGroup" }).txt("false");

  return rootHashTree;
};

// Function to create CacheManager element
const createCacheManager = (rootHashTree) => {
  const cacheManager = rootHashTree.ele("CacheManager", {
    guiclass: "CacheManagerGui",
    testclass: "CacheManager",
    testname: "HTTP Cache Manager",
  });

  cacheManager.ele("boolProp", { name: "clearEachIteration" }).txt("true");
  cacheManager.ele("boolProp", { name: "useExpires" }).txt("false");
  cacheManager.ele("boolProp", { name: "CacheManager.controlledByThread" }).txt("false");

  return rootHashTree;
};

const createDebugSampler = (rootHashTree) => {
  const debugSampler = rootHashTree.ele("DebugSampler", {
    guiclass: "TestBeanGUI",
    testclass: "DebugSampler",
    testname: "Debug Sampler",
  });

  debugSampler.ele("boolProp", { name: "displayJMeterProperties" }).txt("false");
  debugSampler.ele("boolProp", { name: "displayJMeterVariables" }).txt("true");
  debugSampler.ele("boolProp", { name: "displaySystemProperties" }).txt("false");

  return rootHashTree;
};

const createViewResultsTree = (rootHashTree) => {
  const viewResultsTree = rootHashTree.ele("ResultCollector", {
    guiclass: "ViewResultsFullVisualizer",
    testclass: "ResultCollector",
    testname: "View Results Tree",
  });

  viewResultsTree.ele("boolProp", { name: "ResultCollector.error_logging" }).txt("false");
  const objProp = viewResultsTree.ele("objProp");

  objProp.ele("name").txt("saveConfig");
  const value = objProp.ele("value", {
    class: "SampleSaveConfiguration",
  });

  value.ele("time").txt("true");
  value.ele("latency").txt("true");
  value.ele("timestamp").txt("true");
  value.ele("success").txt("true");
  value.ele("label").txt("true");
  value.ele("code").txt("true");
  value.ele("message").txt("true");
  value.ele("threadName").txt("true");
  value.ele("dataType").txt("true");
  value.ele("encoding").txt("false");
  value.ele("assertions").txt("true");
  value.ele("subresults").txt("true");
  value.ele("responseData").txt("false");
  value.ele("samplerData").txt("false");
  value.ele("xml").txt("false");
  value.ele("fieldNames").txt("true");
  value.ele("responseHeaders").txt("false");
  value.ele("requestHeaders").txt("false");
  value.ele("responseDataOnError").txt("false");
  value.ele("saveAssertionResultsFailureMessage").txt("true");
  value.ele("assertionsResultsToSave").txt("0");
  value.ele("bytes").txt("true");
  value.ele("sentBytes").txt("true");
  value.ele("url").txt("true");
  value.ele("threadCounts").txt("true");
  value.ele("idleTime").txt("true");
  value.ele("connectTime").txt("true");

  viewResultsTree.ele("stringProp", {
    name: "filename",
  });

  return rootHashTree;
};

const createThreadGroup = (rootHashTree, testName) => {
  const threadGroup = rootHashTree.ele("ThreadGroup", {
    guiclass: "ThreadGroupGui",
    testclass: "ThreadGroup",
    testname: testName,
  });

  threadGroup
    .ele("intProp", {
      name: "ThreadGroup.num_threads",
    })
    .txt("1");
  threadGroup
    .ele("intProp", {
      name: "ThreadGroup.ramp_time",
    })
    .txt("1");
  threadGroup
    .ele("boolProp", {
      name: "ThreadGroup.same_user_on_next_iteration",
    })
    .txt("true");
  threadGroup
    .ele("stringProp", {
      name: "ThreadGroup.on_sample_error",
    })
    .txt("continue");

  const elementProp = threadGroup
    .ele("elementProp", {
      name: "ThreadGroup.main_controller",
      elementType: "LoopController",
      guiclass: "LoopControlPanel",
      testclass: "LoopController",
      testname: "Loop Controller",
    })
    .txt("continue");

  elementProp
    .ele("stringProp", {
      name: "LoopController.loops",
    })
    .txt("1");
  elementProp
    .ele("boolProp", {
      name: "LoopController.continue_forever",
    })
    .txt("false");
};

const createTransactionController = (rootHashTree, transactionName) => {
  const transactionController = rootHashTree.ele("TransactionController", {
    guiclass: "TransactionControllerGui",
    testclass: "TransactionController",
    testname: transactionName,
  });

  transactionController.ele("boolProp", { name: "TransactionController.parent" }).txt("true");
  transactionController.ele("boolProp", { name: "TransactionController.includeTimers" }).txt("false");

  return rootHashTree;
};

const createSamplers = (rootHashTree, samplers = [], headers = []) => {
  const samplerHashTree = rootHashTree.ele("hashTree");
  samplers.forEach((sampler, index) => {
    const samplerElement = samplerHashTree.ele("HTTPSamplerProxy", {
      guiclass: "HttpTestSampleGui",
      testclass: "HTTPSamplerProxy",
      testname: sampler.testname,
    });

    samplerElement.ele("stringProp", { name: "HTTPSampler.domain" }).txt(sampler.domain);
    samplerElement.ele("stringProp", { name: "HTTPSampler.port" }).txt("0");
    samplerElement.ele("stringProp", { name: "HTTPSampler.protocol" }).txt("https");
    samplerElement.ele("stringProp", { name: "HTTPSampler.path" }).txt(sampler.path);
    samplerElement.ele("boolProp", { name: "HTTPSampler.follow_redirects" }).txt("true");
    samplerElement.ele("stringProp", { name: "HTTPSampler.method" }).txt(sampler.method);
    samplerElement.ele("boolProp", { name: "HTTPSampler.use_keepalive" }).txt("true");
    samplerElement.ele("boolProp", { name: "HTTPSampler.postBodyRaw" }).txt("false");

    const argumentsElement = samplerElement.ele("elementProp", {
      name: "HTTPsampler.Arguments",
      elementType: "Arguments",
      guiclass: "HTTPArgumentsPanel",
      testclass: "Arguments",
      testname: "User Defined Variables",
    });

    argumentsElement.ele("collectionProp", { name: "Arguments.arguments" });

    const headerManagerHashTree = samplerHashTree.ele("hashTree");

    const headerManager = headerManagerHashTree.ele("HeaderManager", {
      guiclass: "HeaderPanel",
      testclass: "HeaderManager",
      testname: "HTTP Header manager",
      enabled: "true",
    });

    const collectionProp = headerManager.ele("collectionProp", {
      name: "HeaderManager.headers",
    });

    headers[index].forEach((header) => {
      let elementProp = collectionProp.ele("elementProp", {
        name: header.name,
        elementType: "Header",
      });

      elementProp
        .ele("stringProp", {
          name: "Header.name",
        })
        .txt(header.name);

      elementProp
        .ele("stringProp", {
          name: "Header.value",
        })
        .txt(header.value);
    });
    headerManagerHashTree.ele("hashTree"); // Add <hashTree/> for HeaderManager
  });
};

// Main function to generate JMeter XML
function generateJMeterXml() {
  // Create the root element
  const root = builder
    .create("jmeterTestPlan", {
      version: "1.0",
      encoding: "UTF-8",
    })
    .att({
      version: "1.0",
      properties: "5.0",
      jmeter: "5.6.3",
    });

  // Create list of samplers to attach to a transaction controller
  const samplers1 = [
    {
      testname: "Launch_URL-0",
      domain: "test.com",
      path: "/index.htm",
      method: "GET",
    },
    {
      testname: "Launch_URL-1",
      domain: "test.com",
      path: "/test",
      method: "GET",
    },
  ];

  const headers1 = [
    [
      {
        name: "Host",
        value: "test.com",
      },
      {
        name: "Connection",
        value: "keep-alive",
      },
      {
        name: "Cache-Control",
        value: "max-age=0",
      },
      {
        name: "sec-ch-ua",
        value: `"Google Chrome";v="131", "Chromium";v="131", "Not_A Brand";v="24"`,
      },
      {
        name: "sec-ch-ua-mobile",
        value: `?0`,
      },
      {
        name: "sec-ch-ua-platform",
        value: `Windows`,
      },
      {
        name: "Upgrade-Insecure-Requests",
        value: `1`,
      },
      {
        name: "User-Agent",
        value: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36`,
      },
      {
        name: "Accept",
        value: `text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7`,
      },
      {
        name: "Sec-Fetch-Site",
        value: `none`,
      },
      {
        name: "Sec-Fetch-User",
        value: `?1`,
      },
      {
        name: "Sec-Fetch-Dest",
        value: `document`,
      },
    ],
    [
      {
        name: "Host",
        value: "test",
      },
      {
        name: "Connection",
        value: "test",
      },
      {
        name: "Cache-Control",
        value: "test",
      },
    ],
  ];

  // Create list of samplers to attach to a transaction controller
  const samplers2 = [
    {
      testname: "Register-0",
      domain: "test.com",
      path: "/register",
      method: "GET",
    },
    {
      testname: "Register-1",
      domain: "test.com",
      path: "/register_user",
      method: "GET",
    },
  ];

  const headers2 = [
    [
      {
        name: "Host",
        value: "test.com",
      },
      {
        name: "Connection",
        value: "keep-alive",
      },
      {
        name: "Cache-Control",
        value: "max-age=0",
      },
      {
        name: "sec-ch-ua",
        value: `"Google Chrome";v="131", "Chromium";v="131", "Not_A Brand";v="24"`,
      },
      {
        name: "sec-ch-ua-mobile",
        value: `?0`,
      },
      {
        name: "sec-ch-ua-platform",
        value: `Windows`,
      },
      {
        name: "Upgrade-Insecure-Requests",
        value: `1`,
      },
      {
        name: "User-Agent",
        value: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36`,
      },
      {
        name: "Accept",
        value: `text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7`,
      },
      {
        name: "Sec-Fetch-Site",
        value: `none`,
      },
      {
        name: "Sec-Fetch-User",
        value: `?1`,
      },
      {
        name: "Sec-Fetch-Dest",
        value: `document`,
      },
    ],
    [
      {
        name: "Host",
        value: "test",
      },
      {
        name: "Connection",
        value: "test",
      },
      {
        name: "Cache-Control",
        value: "test",
      },
    ],
  ];

  const rootHashTree = root.ele("hashTree");

  createTestPlan(rootHashTree);

  const parentHashTree = rootHashTree.ele("hashTree");

  // Create user defined variables, cookie manager, cache manager
  createUserDefinedVariables(parentHashTree);
  parentHashTree.ele("hashTree");
  createCookieManager(parentHashTree);
  parentHashTree.ele("hashTree");
  createCacheManager(parentHashTree);
  parentHashTree.ele("hashTree");

  // Create thread group
  createThreadGroup(parentHashTree, "Test name");

  // Create a new hashTree specifically for transaction controllers and samplers
  const transactionHashTree = parentHashTree.ele("hashTree");

  // Create transaction controller 1
  const transactionName1 = "Launch_URL";
  createTransactionController(transactionHashTree, transactionName1);
  createSamplers(transactionHashTree, samplers1, headers1);

  // Create transaction controller 2
  const transactionName2 = "Register";
  createTransactionController(transactionHashTree, transactionName2);
  createSamplers(transactionHashTree, samplers2, headers2);

  createDebugSampler(transactionHashTree);
  transactionHashTree.ele("hashTree");

  createViewResultsTree(transactionHashTree);
  transactionHashTree.ele("hashTree");

  // Convert the builder object to an XML string
  const xmlString = root.end({ pretty: true });

  // Write the generated XML to a file
  fs.writeFileSync(fileName, xmlString, "utf8");
  console.log("File generated");
}

// Run the function to generate the XML
generateJMeterXml();
