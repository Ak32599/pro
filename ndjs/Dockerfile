FROM node:18 AS builder 
WORKDIR /ndjs 
# Copy only dependency files first (better caching) 
COPY package*.json  ./ 
RUN  npm  install  --production 
# Copy application source code 
COPY  server.js . 
# Stage 2: Runtime (small image) 
FROM  node:18-slim 
WORKDIR  /ndjs
# Copy only required files from builder 
COPY  --from=builder  /ndjs/node_modules  ./node_modules 
COPY  --from=builder  /ndjs/server.js . 
CMD ["node", "server.js"] 