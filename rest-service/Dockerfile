FROM node:20 AS build-env
ADD package.json /app/package.json
ADD package-lock.json /app/package-lock.json
ADD tsconfig.json /app/tsconfig.json
ADD src /app/src
WORKDIR /app
RUN npm install
RUN npm run build

FROM gcr.io/distroless/nodejs20-debian11
COPY --from=build-env /app/dist /app/dist
COPY --from=build-env /app/package.json /app/package.json
COPY --from=build-env /app/package-lock.json /app/package-lock.json
COPY --from=build-env /app/node_modules /app/node_modules
WORKDIR /app
EXPOSE 3000
CMD ["dist/index.js"]
