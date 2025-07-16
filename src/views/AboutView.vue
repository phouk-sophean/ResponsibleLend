<template>
  <div class="max-w-4xl mx-auto space-y-8">
    <!-- Hero Section -->
    <div class="text-center">
      <h1 class="text-4xl font-bold text-slate-800 mb-4">About Responsible Lending</h1>
      <p class="text-xl text-slate-600 leading-relaxed max-w-3xl mx-auto">
        Our mission is to promote financial wellness and prevent over-indebtedness through responsible lending practices and transparent risk assessment.
      </p>
    </div>

    <!-- Main Content -->
    <div class="grid md:grid-cols-2 gap-8">
      <!-- What We Do -->
      <div class="bg-white rounded-xl shadow-sm border border-slate-200 p-8">
        <div class="flex items-center mb-6">
          <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center mr-4">
            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
            </svg>
          </div>
          <h2 class="text-2xl font-bold text-slate-800">What We Do</h2>
        </div>
        
        <div class="space-y-4">
          <div class="flex items-start">
            <div class="w-2 h-2 bg-blue-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
            <p class="text-slate-600">
              <strong class="text-slate-800">Risk Assessment:</strong> We evaluate loan applications using the debt-to-income ratio to ensure sustainable borrowing.
            </p>
          </div>
          <div class="flex items-start">
            <div class="w-2 h-2 bg-blue-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
            <p class="text-slate-600">
              <strong class="text-slate-800">Financial Protection:</strong> Our 40% DTI threshold helps prevent borrowers from taking on excessive debt.
            </p>
          </div>
          <div class="flex items-start">
            <div class="w-2 h-2 bg-blue-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
            <p class="text-slate-600">
              <strong class="text-slate-800">Transparency:</strong> All calculations and decisions are clearly explained to promote financial literacy.
            </p>
          </div>
        </div>
      </div>

      <!-- How It Works -->
      <div class="bg-white rounded-xl shadow-sm border border-slate-200 p-8">
        <div class="flex items-center mb-6">
          <div class="w-12 h-12 bg-green-100 rounded-xl flex items-center justify-center mr-4">
            <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
            </svg>
          </div>
          <h2 class="text-2xl font-bold text-slate-800">How It Works</h2>
        </div>

        <div class="space-y-6">
          <div class="flex items-start">
            <div class="w-8 h-8 bg-green-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
              <span class="text-sm font-bold text-green-600">1</span>
            </div>
            <div>
              <h3 class="font-semibold text-slate-800 mb-1">Application Submission</h3>
              <p class="text-sm text-slate-600">Borrowers provide their monthly income, expenses, and requested loan amount.</p>
            </div>
          </div>

          <div class="flex items-start">
            <div class="w-8 h-8 bg-green-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
              <span class="text-sm font-bold text-green-600">2</span>
            </div>
            <div>
              <h3 class="font-semibold text-slate-800 mb-1">Risk Calculation</h3>
              <p class="text-sm text-slate-600">Our system calculates the debt-to-income ratio and assesses financial capacity.</p>
            </div>
          </div>

          <div class="flex items-start">
            <div class="w-8 h-8 bg-green-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
              <span class="text-sm font-bold text-green-600">3</span>
            </div>
            <div>
              <h3 class="font-semibold text-slate-800 mb-1">Instant Decision</h3>
              <p class="text-sm text-slate-600">Applications are approved or rejected instantly based on responsible lending criteria.</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Key Features -->
    <div class="bg-gradient-to-r from-slate-50 to-blue-50 rounded-xl p-8">
      <h2 class="text-2xl font-bold text-slate-800 mb-8 text-center">Key Features</h2>
      
      <div class="grid md:grid-cols-3 gap-6">
        <div class="text-center">
          <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"></path>
            </svg>
          </div>
          <h3 class="font-bold text-slate-800 mb-2">Secure & Private</h3>
          <p class="text-sm text-slate-600">Your financial information is processed securely and never stored permanently.</p>
        </div>

        <div class="text-center">
          <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-8 h-8 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"></path>
            </svg>
          </div>
          <h3 class="font-bold text-slate-800 mb-2">Data-Driven</h3>
          <p class="text-sm text-slate-600">Decisions are based on proven financial metrics and responsible lending standards.</p>
        </div>

        <div class="text-center">
          <div class="w-16 h-16 bg-purple-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-8 h-8 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
            </svg>
          </div>
          <h3 class="font-bold text-slate-800 mb-2">Instant Results</h3>
          <p class="text-sm text-slate-600">Get immediate feedback on your loan application with clear explanations.</p>
        </div>
      </div>
    </div>

    <!-- Statistics -->
    <div class="bg-white rounded-xl shadow-sm border border-slate-200 p-8">
      <h2 class="text-2xl font-bold text-slate-800 mb-8 text-center">Why 40% DTI Matters</h2>
      
      <div class="grid md:grid-cols-2 gap-8">
        <div>
          <h3 class="text-lg font-semibold text-slate-800 mb-4">Financial Health Indicators</h3>
          <div class="space-y-4">
            <div class="flex justify-between items-center p-3 bg-green-50 rounded-lg">
              <span class="text-sm font-medium text-slate-700">DTI Below 20%</span>
              <span class="text-sm font-bold text-green-600">Excellent</span>
            </div>
            <div class="flex justify-between items-center p-3 bg-blue-50 rounded-lg">
              <span class="text-sm font-medium text-slate-700">DTI 20% - 40%</span>
              <span class="text-sm font-bold text-blue-600">Good</span>
            </div>
            <div class="flex justify-between items-center p-3 bg-amber-50 rounded-lg">
              <span class="text-sm font-medium text-slate-700">DTI 40% - 50%</span>
              <span class="text-sm font-bold text-amber-600">Caution</span>
            </div>
            <div class="flex justify-between items-center p-3 bg-red-50 rounded-lg">
              <span class="text-sm font-medium text-slate-700">DTI Above 50%</span>
              <span class="text-sm font-bold text-red-600">High Risk</span>
            </div>
          </div>
        </div>

        <div>
          <h3 class="text-lg font-semibold text-slate-800 mb-4">Benefits of Responsible Lending</h3>
          <div class="space-y-3">
            <div class="flex items-center">
              <svg class="w-5 h-5 text-green-500 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
              </svg>
              <span class="text-sm text-slate-600">Prevents financial stress and bankruptcy</span>
            </div>
            <div class="flex items-center">
              <svg class="w-5 h-5 text-green-500 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
              </svg>
              <span class="text-sm text-slate-600">Maintains healthy credit scores</span>
            </div>
            <div class="flex items-center">
              <svg class="w-5 h-5 text-green-500 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
              </svg>
              <span class="text-sm text-slate-600">Promotes long-term financial stability</span>
            </div>
            <div class="flex items-center">
              <svg class="w-5 h-5 text-green-500 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
              </svg>
              <span class="text-sm text-slate-600">Reduces default rates for lenders</span>
            </div>
            <div class="flex items-center">
              <svg class="w-5 h-5 text-green-500 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
              </svg>
              <span class="text-sm text-slate-600">Builds trust in the lending ecosystem</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Contact Information -->
    <div class="bg-gradient-to-r from-blue-600 to-indigo-700 rounded-xl p-8 text-white text-center">
      <h2 class="text-2xl font-bold mb-4">Questions About Responsible Lending?</h2>
      <p class="text-blue-100 mb-6 max-w-2xl mx-auto">
        Our team is committed to promoting financial wellness and helping you understand responsible borrowing practices.
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <a href="mailto:support@responsiblelend.com" class="bg-white text-blue-600 px-6 py-3 rounded-lg font-semibold hover:bg-blue-50 transition-colors">
          Contact Support
        </a>
        <a href="#" class="border border-white text-white px-6 py-3 rounded-lg font-semibold hover:bg-white hover:text-blue-600 transition-colors">
          Learn More
        </a>
      </div>
    </div>
  </div>
</template>